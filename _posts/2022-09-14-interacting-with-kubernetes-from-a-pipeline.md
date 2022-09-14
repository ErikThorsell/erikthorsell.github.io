When you work with Kubernetes you likely use `kubectl` from your local development environment.
In your pipeline, however, you likely want to use a Service Account.
This post outlines how to create such a Service Account and how to make use of it in a GitHub Workflow.

# What we'll do

1. Create a Service Account in the Kubernetes cluster
2. Create a Secret (Service Account Token)
3. Extract the secret parts of the Secret
4. Create a Role to allow the SA to do stuff in the Cluster
5. Add everything to a GitHub Workflow

## Gotcha

Previously (before Kubernetes 1.24) the SA Secret was automatically created [LINK](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.24.md#urgent-upgrade-notes).
That is no longer the case, which is why we need to do (2), above.

## Create Service Account

```bash
kubectl -n your-namespace create sa github-robot
```

## Create a Secret for the Service Account

Apply the following using `kubectl`:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: github-robot-secret
  namespace: your-namespace
  annotations:
    kubernetes.io/service-account.name: github-robot
type: kubernetes.io/service-account-token
```

## Fetch the secret parts of the Secret

_Note that we decode both secrets. We will put them in a decoded state in GitHub Secrets._

First, we fetch the `ca.crt`.

```bash
kubectl -n your-namespace get secret github-robot-secret -o json | jq -r '.data["ca.crt"]' | base64 --decode
```

Then we need the `token`:

```bash
kubectl -n your-namespace get secret github-robot-secret -o json | jq -r '.data["token"]' | base64 --decode
```

# Create Role

Apply the following using `kubectl`:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: github-robot-role
  namespace: your-namespace
rules:
  - apiGroups:
      - ""
      - apps
      - extensions
    resources:
      - "*"
    verbs:
      - "*"
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: github-robot-role-binding
  namespace: your-namespace
subjects:
  - kind: ServiceAccount
    name: github-robot
roleRef:
  kind: Role
  name: github-robot-role
  apiGroup: rbac.authorization.k8s.io
```

## Create the config in your Workflow

After you have addde the `ca.crt` and `token` to your GitHub Secrets you can use the following step
to setup a config in your workflow.

```yaml
- name: Set Kubernetes cluster context
  run: |
    echo "${{ secrets.AKS_GITHUB_ROBOT_CA_CRT }}" > ${{ runner.temp }}/ca.crt
    kubectl config set-cluster ${{ secrets.AKS_CLUSTER_NAME }} --server=${{ secrets.AKS_SERVER }} --certificate-authority=${{ runner.temp }}/ca.crt --embed-certs=true
    kubectl config set-credentials github-robot --token=${{ secrets.AKS_GITHUB_ROBOT_TOKEN }}
    kubectl config set-context ${{ secrets.AKS_CONTEXT }} --cluster=${{ secrets.AKS_CLUSTER_NAME }} --user=github-robot --namespace=idp
    kubectl config use-context ${{ secrets.AKS_CONTEXT }}
```
