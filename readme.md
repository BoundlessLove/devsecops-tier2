
AIM: Towards Azure Kubernetes CI/CD setup.

14 April 2026 - Under Construction

## Version 0.1
19 April 2026 17:00 - Working locally on Docker desktop with:


# local dev

a. Pre req: Open Docker Desktop and start containers.

i. Assumption: Your Kubernetes setup is running a Service that uses the load balancer.  

i.   [Navigate to your project in powershell]

ii.  Create Kubernetes cluster k3d cluster create aks-local --config k3d-aks-local.yaml

iii. Confirm cluster creation k3d cluster list

iv.  Start cluster 'k3d cluster start [cluster name]'
 

b. Deploy Service on Kubernetes Cluster

i.   cd app

ii.  docker build -t aks-demo:v1 .

iii. cd ..

iv.  k3d image import aks-demo:v1 -c aks-local

v.   kubectl apply -f k8s/deployment.local.yaml

vi.  kubectl apply -f k8s/service.yaml

c. Verify deployment and launch

i. kubectl get pods

ii. kubectl get svc aks-demo-service. You should see service type of load balancer.

iii. kubectl port-forward svc/aks-demo-service 8080:8080

iv. [Navigate to] http://localhost:8080.


## Version 0.2
19 April 2026 19:37 - Pre-req is creating an Azure Container Registry (ACR) and an Azure Kubernetes Cluster (containing the ACR). First attempt at CICD AKS. 
