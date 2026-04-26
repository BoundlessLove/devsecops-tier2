
AIM: Towards Azure Kubernetes CI/CD setup.

14 April 2026 - Under Construction

## Version 0.1
19 April 2026 17:00 - Working locally on Docker desktop with:


# local dev

## New Cluster in Windows

a. Create cluster with Load Balancer

<i>Pre req: Launch Docker Desktop.</i>

<i>Assumption: Your Kubernetes setup is running a Service that uses the load balancer.  </i>

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

ii. kubectl get svc aks-demo-service. 

You should see service type of load balancer. It is a traefik load balancer. You can see it via:

- kubectl get pods -n kube-system | findstr traefik

iv. [Navigate to] http://localhost:8080.


## Existing Cluster

a. Start cluster

<i>Pre req: Open Docker Desktop.</i>

i. Confirm cluster creation by running "k3d cluster list",

ii.  Start cluster 'k3d cluster start [cluster name]',

b. Verify deployment and launch

i. kubectl get pods

ii. kubectl get svc aks-demo-service. You should see service type of load balancer. It is a traefik load balancer. You can see it via:

- kubectl get pods -n kube-system | findstr traefik

iv. [Navigate to] http://localhost:8080.



## Version 0.2
19 April 2026 19:37 - Pre-req is creating an Azure Container Registry (ACR) and an Azure Kubernetes Cluster (containing the ACR). First attempt at CICD AKS. 


## Version 0.3
24 April 2026 16:36 - Kubernetes working locally with k3d's Traefik load balancer. Steps to setup have been documented in Readme.md file under heading 'local dev'.  

### Version 0.3.1
24 April 2026 16:39 - Added identification of the load balancer as a 'traefik' one - automatically generated in k3d.

## Version 0.4
26 April 2026 20:12 - Kubernetes working locally with https from domain staging.systematicdefence.tech. It uses the following model:

- Cloudflare → Tunnel → cloudflared → aks-demo-service → Pods

![Working https Screenshot](./screenshots/CloudfareTalkingToAKS-Service.jpg)