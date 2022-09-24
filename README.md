# hands-on-assignment-1
A public repository for hands-on assignment part 1  
This repo workflows use helm3 to deploy simple nodejs web service to GKE cluster on GCP.  
However, as I have not set up a GKE cluster, the workflows are expected to fail.

## Run web-server locally
### Dependencies to run web-server on local
- node version v16.0.0
- Docker version 20.10.8
- npm version 7.10.0

### Run web-server using Docker
- Start Docker service
- Build docker image using `docker build -t web-server:local .`
- Run docker container using `docker run --rm -p 8080:8080 web-server:local`
- Test with `curl localhost:8080`, you should receive `Hello World!` response

## Deploy to Kubernetes from local machine
### Dependencies to deploy on Kubernetes
- Helm version 3.7.1
- Docker version 20.10.8

### Deploy to Kubernetes
- Build and push image to registry
- Change `image` field in `helm-values/development.yaml` to the image you just pushed to the registry
- Deploy to Kubernetes cluseter using `helm upgrade --install web-app ./helm-templates -f helm-values/development.yaml`

## To deploy using Githubs Actions workflows
### Deploy to development environment
- Checkout a `feature-branch` off from `master` branch
- When finish `feature-branch`, merge locally to `development`
- Push `development`, the workflow will trigger and deploy to development environment

### Deploy to development staging
- Open a pull request from `feature-branch` into `master`, approve and merge as usual
- Tag and release `master`, for example v1.0.0
- The workflow will trigger and deploy to staging environment
- A manual approval is required to deploy to production
- The workflow will automatically open an issue in the repo
- To approve, the responsible persion (currently is me TanawatChans) will have to comment "approved" in the issue
- The workflow will then deploy to production
