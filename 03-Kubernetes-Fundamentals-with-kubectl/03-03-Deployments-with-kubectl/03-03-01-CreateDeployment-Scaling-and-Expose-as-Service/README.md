# Kubernetes - Deployment

## Step-01: Introduction to Deployments
- What is a Deployment?
- A Deployment provides declarative updates for Pods and ReplicaSets.

  - You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

- The following are typical use cases for Deployments:

  - Create a Deployment to rollout a ReplicaSet. The ReplicaSet creates Pods in the background. Check the status of the rollout to see if it succeeds or not.
  - Declare the new state of the Pods by updating the PodTemplateSpec of the Deployment. A new ReplicaSet is created and the Deployment manages moving the Pods from the old ReplicaSet to the new one at a controlled rate. Each new ReplicaSet updates the revision of the Deployment.
  - Rollback to an earlier Deployment revision if the current state of the Deployment is not stable. Each rollback updates the revision of the Deployment.
  - Scale up the Deployment to facilitate more load.
  - Pause the rollout of a Deployment to apply multiple fixes to its PodTemplateSpec and then resume it to start a new rollout.
  - Use the status of the Deployment as an indicator that a rollout has stuck.
  - Clean up older ReplicaSets that you don't need anymore.
Creating a Deployment
- What all we can do using Deployment?
- Create a Deployment
- Scale the Deployment
- Expose the Deployment as a Service

## Step-02: Create Deployment
- Create Deployment to rollout a ReplicaSet
- Verify Deployment, ReplicaSet & Pods
- **Docker Image Location:** https://hub.docker.com/repository/docker/stacksimplify/kubenginx
```
# Create Deployment
kubectl create deployment <Deplyment-Name> --image=<Container-Image>
kubectl create deployment my-first-deployment --image=stacksimplify/kubenginx:1.0.0 

# Verify Deployment
kubectl get deployments
kubectl get deploy 

# Describe Deployment
kubectl describe deployment <deployment-name>
kubectl describe deployment my-first-deployment

# Verify ReplicaSet
kubectl get rs

# Verify Pod
kubectl get po
```
## Step-03: Scaling a Deployment
- Scale the deployment to increase the number of replicas (pods)
```
# Scale Up the Deployment
kubectl scale --replicas=10 deployment/<Deployment-Name>
kubectl scale --replicas=10 deployment/my-first-deployment 

# Verify Deployment
kubectl get deploy

# Verify ReplicaSet
kubectl get rs

# Verify Pods
kubectl get po

# Scale Down the Deployment
kubectl scale --replicas=2 deployment/my-first-deployment 
kubectl get deploy
```

## Step-04: Expose Deployment as a Service
- Expose **Deployment** with a service (LoadBalancer Service) to access the application externally (from internet)
```
# Expose Deployment as a Service
kubectl expose deployment <Deployment-Name>  --type=LoadBalancer --port=80 --target-port=80 --name=<Service-Name-To-Be-Created>
kubectl expose deployment my-first-deployment --type=LoadBalancer --port=80 --target-port=80 --name=my-first-deployment-service

# Get Service Info
kubectl get svc

```
- **Access the Application using Public IP**
```
http://<External-IP-from-get-service-output>
```
