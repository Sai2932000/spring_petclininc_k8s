Spring PetClinic Kubernetes Deployment

This repository demonstrates how to deploy the Spring PetClinic application on Kubernetes using containerized workloads and namespace-level resource governance.

The Spring PetClinic project is a well-known sample application used to demonstrate how the Spring ecosystem can be used to build real-world applications.

This project focuses on the infrastructure and deployment side, including:

Docker containerization

Kubernetes deployments

Resource management

Namespace isolation

Architecture
Kubernetes Cluster
│
├── Namespace: dev-ns
│
├── ResourceQuota
│
├── LimitRange
│
├── Deployment (Spring PetClinic)
│       └── 4 Pods
│
└── Service (NodePort)
        └── External access
Docker Image

The application container image used in this deployment was built and published by me.

sai8032/sai_petclinic:1.0
Kubernetes Resources

This project contains the following Kubernetes manifests:

Namespace

Creates an isolated environment for the application.

K8S/ns/dev-ns.yaml
ResourceQuota

Controls resource consumption inside the namespace.

Limits applied:

Pods

CPU requests

Memory requests

Services

PVCs

K8S/quotas/dev_quota.yaml
LimitRange

Defines default resource requests and limits for containers.

K8S/limits/dev_limit_range.yaml
Deployment

Deploys the Spring Boot application using 4 replicas.

Features:

Rolling updates

Resource requests and limits

Containerized application

app/deployment.yaml
Service

Exposes the application externally using NodePort.

app/service.yaml
Deployment Steps
1 Clone Repository
git clone https://github.com/Sai2932000/spring_petclininc_k8s.git
cd spring_petclininc_k8s
2 Create Namespace
kubectl apply -f K8S/ns/dev-ns.yaml
3 Apply Resource Policies
kubectl apply -f K8S/limits/dev_limit_range.yaml
kubectl apply -f K8S/quotas/dev_quota.yaml
4 Deploy Application
kubectl apply -f app/deployment.yaml
5 Expose Application
kubectl apply -f app/service.yaml
Verify Deployment

Check resources:

kubectl get all -n dev-ns

Check pods:

kubectl get pods -n dev-ns

Check services:

kubectl get svc -n dev-ns
Access the Application

Once the service is created, the application will be available via NodePort.

Example:

http://<NodeIP>:30001
Troubleshooting Example

During testing, a CrashLoopBackOff occurred due to OOMKilled containers.

Root cause:

Container memory limit was too low.

Solution:

Adjusted memory limits in the deployment configuration.

This helped reinforce practical Kubernetes debugging skills.

Technologies Used

Kubernetes

Docker

Spring Boot

kubectl

ResourceQuota

LimitRange

NodePort Service

Learning Outcomes

Through this project I practiced:

Kubernetes deployments

Namespace resource governance

Pod lifecycle debugging

CrashLoopBackOff troubleshooting

Container resource management

Rolling updates

Future Improvements

Horizontal Pod Autoscaler (HPA)

Ingress controller

Helm charts

GitOps deployment (ArgoCD / Flux)

Author

Sai Thumma

GitHub
https://github.com/Sai2932000
