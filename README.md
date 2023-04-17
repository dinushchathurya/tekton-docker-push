### Build and Push Docker image to Docker Hub using Tekton pipeline

This is a simple sample project to demonstrate how to build and push a Docker image to Docker Hub using Tekton pipeline.

#### Used Tekton resources in this project

- git-clone task [https://hub.tekton.dev/tekton/task/git-clone]
- buildah task [https://hub.tekton.dev/tekton/task/buildah]

#### Folder Structure

- app/ 
  - Dockerfile
  - index.js
  - package.json
- policy/ 
  - READEME.md
  - trust-policy.json
- resources/ 
    - dockerhub-secret.yaml
    - role-binding.yaml
    - role.yaml
    - service-account.yaml
- tekton/ 
    - pipeline-runs/
        - pipeline-run.yaml
    - pipelines/
        - pipeline.yaml
.gitignore
README.md


#### Required configuration

All the required configuration is in the `resources` folder.

- Create a secret with your Docker Hub credentials
- Create ServiceAccount with the secret
- Create Role and RoleBinding to allow the ServiceAccount to create resources in the namespace

You need to apply the above resources before running the pipeline. You use the below command to apply the resources.

```bash
kubectl apply -f resources/
```

#### Troubleshooting

- If you get an error like this:

error while running "VolumeBinding" prebind plugin for pod "app": Failed to bind volumes: timed out waiting for the condition

You can follow the steps in the below link to fix it
[https://github.com/dinushchathurya/tekton-docker-push/blob/master/policy/README.md]   