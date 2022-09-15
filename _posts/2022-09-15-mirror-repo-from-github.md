---
title: Mirror GitHub repository to Azure DevOps
---

At a current client, we are migrating from Azure DevOps to GitHub.
The DevOps Team (responsible for promoting and training developers in DevOps) was quick to adopt the new platform,
but transformation takes time and many developers are still using the old Azure DevOps instance.

We want to make it easy for everyone to get access to a repository where we write DevOps related documentation and we
figured the best thing to do was to mirror our GitHub repository to Azure DevOps.
That way we know that all developers have access to the same information, regardless of where in their transformation
journey they are.


# The workflow

```yaml
name: "Mirror repository to Azure DevOps"

on: push

jobs:
  mirror:
    name: Mirror repository to Azure DevOps
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Setup SSH Config
        run: |
          mkdir -p ~/.ssh/
          echo "${{"{{ secrets.PRIVATE_RSA "}}}}" > ~/.ssh/ado_rsa
          cat << EOF >> ~/.ssh/config
          Host         ssh.dev.azure.com
          IdentityFile ~/.ssh/ado_rsa
          EOF
          chmod 700 ~/.ssh
          chmod 600 ~/.ssh/ado_rsa

      - name: Push to ADO
        run: |
          git remote add ado git@ssh.dev.azure.com:v3/organization/project/repo
          git push --force -u ado --all
```

## Noteworthy things

Some things worth commenting on.

#### Clone depth

In order to be able to _push_ a git repository, it is not enough to do a shallow clone (which is the default for the
action).
Setting `fetch-depth: 0` clones the entire repository.

```yaml
- name: Checkout repository
  uses: actions/checkout@v3
  with:
    fetch-depth: 0
```

#### SSH authentication

I could not get git over HTTPS to work.
I started of with HTTPS because I thought it would be easier.
Just do `git push https://$userame:password@url`, right?
Nope...

Instead, I set up a public SSH key -- in Azure DevOps -- for the service account we're using to push the code and wrote
some bash to get git to use the correct key.
The private part of the SSH key is stored as a secret in GitHub.

```yaml
- name: Setup SSH Config
  run: |
    mkdir -p ~/.ssh/
    echo "${{ secrets.PRIVATE_RSA }}" > ~/.ssh/ado_rsa
    cat << EOF >> ~/.ssh/config
    Host         ssh.dev.azure.com
    IdentityFile ~/.ssh/ado_rsa
    EOF
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/ado_rsa
```

Note that a file created using `echo "something" > file` will have permissions `644`, which is too permissive for an
SSH Key.
Hence, we must `chmod` the directory and file we just created.