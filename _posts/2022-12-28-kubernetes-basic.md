---
title: Service-to-service communication in Kubernetes
classes: wide
---

I post this to have a good reference (for myself and others) for a minimal Kubernetes manifest that allows
service-to-service communication.

# The problem

> How could the developer of the microservice `frontend` configure their application such that it can talk to `backend`,
> before either microservice has been deployed?

The detailed functionality of the microservices is not relevant for the example, but it is assumed that `frontend` wants
to make HTTP requests towards `backend`.


# Proposal

By deploying their application as seen below, `frontend` can be configured to communicate with
`http://backend-service`[^port-80-convention], without knowing the `Cluster IP` of the `backend` microservice.
Your DNS server of choice, in Kubernetes, will handle the translation.

### A quick note 

The `frontend-service` exposes a `NodePort`.
This is useful if you run [minikube](https://minikube.sigs.k8s.io/docs/start/), [k3s](https://docs.k3s.io/) or something
similar, and you want to test your deployment locally.
In a production scenario, you should front your `service` with an
[Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) instead of connecting straight to the
`service`.


## Manifests

```yaml
# File: backend.yaml

# Documentation for deployments: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
# kubectl explain --api-version=apps/v1 Deployment
apiVersion: apps/v1
kind: Deployment

# The metadata applies to the deployment itself.
# We give it a name and put the deployment in a namespace.
# http://kubernetes.io/docs/user-guide/labels
metadata:
  name: backend-deployment
  namespace: default

# The specification of the desired behaviour of the Deployment.
spec:
  # Number of desired pods
  replicas: 3
  # Existing ReplicaSets whose pods are selected by this will be the ones affected by this deployment.
  # The label selector is the core grouping primitive in Kubernetes.
  # It must match the pod template's labels below.
  selector:
    matchLabels:
      app: backend

  # Template describes the pods that will be created.
  template:

    # Standard object's metadata.
    # The label app: frontend, is what groups the pod to the Deployment.
    metadata:
      labels: 
        app: backend

    # Specification of the desired behaviour of the Pod.
    spec:
      # List of containers belonging to the pod along with settings for them.
      # We use IfNotPresent to avoid pulling images from a registry if they already exist locally.
      containers:
        - name: backend
          image: backend:latest
          imagePullPolicy: IfNotPresent
          ports:
            - name: "backend-http"
              containerPort: 80

---

# Documentation: https://kubernetes.io/docs/concepts/services-networking/service/
# kubectl explain --api-version=v1 Service
apiVersion: v1
kind: Service

# Metadata concerning the Service
metadata:
  name: backend-service
  namespace: default

# The specification for the Service
spec:
  # Type determines how the Service is exposed.
  # Defaults to ClusterIP.
  type: ClusterIP

  # Route service traffic to pods with label keys and values matching this selector.
  # In the deployment-yaml, the pods are given the same label as the one here.
  selector:
    app: backend

  # There are three ports specified here:
  # port, is the port that will be exposed by this service
  # targetPort, is the name (or number) of the port to access on the pods targeted by the service
  ports:
    - port: 80
      targetPort: backend-http
```

I have omitted the comments that are simply duplicates of the `backend`-YAML-comments.

```yaml
# File: frontend.yaml

apiVersion: apps/v1
kind: Deployment

metadata:
  name: frontend-deployment
  namespace: default

spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend

  template:
    metadata:
      labels: 
        app: frontend

    spec:
      containers:
        - name: frontend
          image: frontend:latest
          imagePullPolicy: IfNotPresent
          ports:
            - name: "frontend-http"
              containerPort: 80

---

apiVersion: v1
kind: Service

metadata:
  name: frontend-service
  namespace: default

spec:
  # Valid options are: ExternalName, ClusterIP, NodePort, and LoadBalancer.
  # https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types
  # We use NodePort here since we want to expose the frontend outside of the cluster.
  # Reaching the service from a browser or using curl is a bit tricky though.
  # You connect using the <Node-IP>:<NodePort>.
  # Retrieve the NodeIP by running: kubectl get nodes -o json | jq -r '.items[0].metadata.annotations."alpha.kubernetes.io/provided-node-ip"'
  # Retrieve the NodePort by running: kubectl get svc frontend-service -o json | jq '.spec.ports[0].nodePort'
  type: NodePort

  selector:
    app: frontend

  ports:
    - port: 8080
      targetPort: frontend-http
```


<!-- --------------------------------------------------------------------------------------------------------------- -->

<!-- FEET NOTES -->
[^port-80-convention]: It is assumed that communication between the pods is made using Port 80.

<!-- REFERENCES -->
[reference]: https://example.com