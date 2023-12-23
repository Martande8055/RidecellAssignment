<div align="center">
  <h1>✨ Guestbook-Go Github Action Workflow ✨</h1> 
</div>

## ✨ Approach
### 1) Created a new GitHub public Repository from [Repository Link](https://github.com/kubernetes/examples/tree/master/guestbook-go)
### 2) Created a container image using the GitHub Action workflow for the above project and Pushed that image to the docker hub.
#### i. Prevented merging anything in the main branch without review.
![image](https://github.com/Martande8055/RidecellAssignment/assets/88831689/ad16a239-0f94-4927-ad8a-81041ba35513)


#### ii. Build container image only when one of the below conditions is true:
##### ✔️ When PR gets merged in the main branch from any other branch.
##### ✔️ When the commit message contains `BUILD_CONTAINER_IMAGE` string
```yaml
...
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
    types:
      - closed

jobs:

  build:
    if: |
      (github.event.pull_request.merged == true) ||
      contains(github.event.head_commit.message, 'BUILD_CONTAINER_IMAGE')

```
## ✨Actions
1. Installed Go in the workflow environment.
2. Installed dependencies needed for building the Go project.
3. Build a Go module.
4. Created repository secrets for DockerHub USERNAME and PASSWORD.
5. Build and push the docker image to DockerHub.

## ✨TEST 
1. Build a container image when PR gets merged in the main branch from any other branch.
   ![image](https://github.com/Martande8055/RidecellAssignment/assets/88831689/04d0bea2-0693-4a01-83b1-ebb49ce9a999)


2. Build a container image When the commit message contains `BUILD_CONTAINER_IMAGE` string.
   ![image](https://github.com/Martande8055/RidecellAssignment/assets/88831689/13ba1172-09d6-47b2-aa28-e21bccac8416)


3. Container image pushed to DockerHub
   ![image](https://github.com/Martande8055/RidecellAssignment/assets/88831689/7b970bc9-e1f4-4ec8-9c57-ec17a3427da3)




## ✨ Steps to Deploy container image to Kubernetes cluster

1. Clone this GitHub Repo i.e [Guestbook-Go](https://github.com/Martande8055/RidecellAssignment.git)
```sh
git clone https://github.com/Martande8055/RidecellAssignment.git
```
2. Run the following commands on your Kubernetes cluster.
```sh
kubectl create -f redis-master-controller.yaml
kubectl create -f redis-master-service.yaml
kubectl create -f redis-replica-controller.yaml
kubectl create -f redis-replica-service.yaml
kubectl create -f guestbook-controller.yaml
kubectl create -f guestbook-service.yaml
```
3. Run the following command to get the URL
```sh
minikube service guestbook
```

## Result 🎉 🎉 
![image](https://github.com/Martande8055/RidecellAssignment/assets/88831689/c3366331-1c42-47f1-83eb-371add90ee63)

![image](https://github.com/Martande8055/RidecellAssignment/assets/88831689/8a9bd765-1c0f-47ae-8f36-520b43abe584)



<!-- Comment to change code and test workflow: 6 -->
