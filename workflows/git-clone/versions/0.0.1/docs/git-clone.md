# clone-s3

## Summary
Clone a repository on the /codefresh/volume diretcory

## Inputs/Outputs

### Inputs
#### Parameters
* CF_REPO_OWNER (required) - the repository you want to clone (for example: https://github.com/codefresh-io/argo-hub)
* CF_REPO_NAME (required)
* CF_BRANCH (optional) - the revision to checkout. defaults to `main`
* GIT_TOKEN_SECRET (optional) - the k8s secret name that contains a key named `token` with the git secret inside it. default to github-token
* KEY (optional) - the key to which the artifact will be pushed. defaults to `{{ workflow.name }}/git-repo`

### Outputs
#### Artifacts
* WORKING_DIR - will contain the cloned repository

## Examples

### task Example
```
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: git-clone-s3
spec:
  entrypoint: main
  templates:
  - name: main
    dag:
      tasks:
      - name: clone
        templateRef:
          name: convert.git-clone.0.0.1
          template: git-clone
        arguments:
          parameters:
          - name: CF_REPO_OWNER
            value: 'codefresh-io'
          - name: CF_REPO_NAME
            value: 'argo-hub'
          - name: CF_BRANCH
            value: 'main'
          - name: GIT_TOKEN_SECRET
            value: 'github-token'
```
