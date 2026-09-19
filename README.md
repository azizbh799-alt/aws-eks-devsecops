# 🚀 AWS EKS DevSecOps Project

A cloud-native DevSecOps project demonstrating the deployment of a containerized full-stack application on **Amazon EKS (Elastic Kubernetes Service)** using **Docker, Kubernetes, NGINX Ingress, and AWS**.

The project focuses on containerization, Kubernetes orchestration, scalability, service communication, and secure cloud deployment practices.

---

## 🏗️ Architecture

```text
                         🌍 Internet
                              │
                              ▼
                    ┌───────────────────┐
                    │   AWS LoadBalancer │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │   NGINX Ingress   │
                    │    Controller     │
                    └─────────┬─────────┘
                              │
                 ┌────────────┴────────────┐
                 │                         │
              "/"                       "/api"
                 │                         │
                 ▼                         ▼
       ┌──────────────────┐      ┌──────────────────┐
       │ Frontend Service │      │ Backend Service  │
       └────────┬─────────┘      └────────┬─────────┘
                │                         │
                ▼                         ▼
       ┌──────────────────┐      ┌──────────────────┐
       │ Frontend Pods    │      │ Backend Pods     │
       │   Replica ×2     │      │   Replica ×2     │
       └──────────────────┘      └──────────────────┘
                │                         │
                └────────────┬────────────┘
                             ▼
                       ☁️ AWS EKS
```

---

## 🛠️ Technologies

| Technology       | Purpose                          |
| ---------------- | -------------------------------- |
| ☁️ AWS EKS       | Kubernetes cluster               |
| 🐳 Docker        | Containerization                 |
| ☸️ Kubernetes    | Container orchestration          |
| 🌐 NGINX Ingress | HTTP routing and external access |
| 🐙 GitHub        | Source code management           |
| 🐧 Linux         | Cloud environment                |
| 📦 Docker Hub    | Container image registry         |
| 🔧 kubectl       | Kubernetes management            |
| ☁️ AWS CLI       | AWS management                   |

---

## 📂 Project Structure

```text
aws-eks-devsecops/
│
├── backend/
│   └── Dockerfile
│
├── frontend/
│   └── Dockerfile
│
├── k8s/
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   └── ingress.yaml
│
├── .gitignore
└── README.md
```

---

## ☁️ AWS Infrastructure

The application is deployed on an Amazon EKS cluster with:

* Kubernetes cluster: `eks-devsecops`
* Kubernetes worker nodes: 2 × `t3.medium`
* Region: `us-east-1`
* NGINX Ingress Controller
* AWS Load Balancer
* Kubernetes Deployments
* Kubernetes ClusterIP Services

---

## 🐳 Docker Images

The application containers are published to Docker Hub.

### Backend

```text
azizx7/backend:v1
```

### Frontend

```text
azizx7/frontend:v6
```

Using Docker Hub was necessary because the AWS Learner Lab environment used for this project restricted access to Amazon ECR.

---

## ☸️ Kubernetes Deployment

The application uses Kubernetes Deployments with two replicas for both frontend and backend.

### Backend

```yaml
replicas: 2
```

### Frontend

```yaml
replicas: 2
```

This provides basic redundancy and demonstrates Kubernetes workload management.

---

## 🌐 Ingress Routing

NGINX Ingress routes incoming HTTP requests to the appropriate Kubernetes service.

```text
/        → frontend-service:80
/api     → backend-service:8000
```

This allows both frontend and backend services to be accessed through a single external entry point.

---

## 🚀 Deployment Commands

### 1. Configure AWS credentials

```bash
aws configure
```

### 2. Connect kubectl to the EKS cluster

```bash
aws eks update-kubeconfig \
  --region us-east-1 \
  --name eks-devsecops
```

### 3. Verify the cluster

```bash
kubectl get nodes
```

### 4. Deploy the backend

```bash
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/backend-service.yaml
```

### 5. Deploy the frontend

```bash
kubectl apply -f k8s/frontend-deployment.yaml
kubectl apply -f k8s/frontend-service.yaml
```

### 6. Deploy the Ingress

```bash
kubectl apply -f k8s/ingress.yaml
```

### 7. Check the application

```bash
kubectl get pods
kubectl get services
kubectl get ingress
```

---

## 🔍 Kubernetes Verification

Check running pods:

```bash
kubectl get pods
```

Check services:

```bash
kubectl get svc
```

Check the Ingress:

```bash
kubectl get ingress
```

Check the NGINX controller:

```bash
kubectl get pods -n ingress-nginx
```

---

## 📈 Scalability

The project uses Kubernetes replicas to provide basic application scalability.

```text
Frontend
├── Pod 1
└── Pod 2

Backend
├── Pod 1
└── Pod 2
```

The number of replicas can be increased with:

```bash
kubectl scale deployment frontend-deployment --replicas=3
kubectl scale deployment backend-deployment --replicas=3
```

---

## 🔐 Security Considerations

Security practices implemented in the project include:

* Kubernetes service isolation
* ClusterIP services for internal communication
* NGINX Ingress for controlled external routing
* Resource requests and limits
* Sensitive files excluded through `.gitignore`
* AWS credentials excluded from Git
* Container images stored in a container registry

> ⚠️ Never commit AWS credentials, access keys, secret keys, `.pem` files, `.env` files, or other sensitive information to GitHub.

---

## 🧪 Useful Commands

### View all resources

```bash
kubectl get all
```

### View deployment status

```bash
kubectl get deployments
```

### Describe a pod

```bash
kubectl describe pod <pod-name>
```

### View pod logs

```bash
kubectl logs <pod-name>
```

### Restart a deployment

```bash
kubectl rollout restart deployment frontend-deployment
kubectl rollout restart deployment backend-deployment
```

---

## 📚 Learning Objectives

This project was built to practice:

* AWS EKS
* Kubernetes
* Docker
* Container orchestration
* Kubernetes networking
* NGINX Ingress
* AWS Load Balancing
* Infrastructure deployment
* Cloud-native application architecture
* DevOps and DevSecOps principles

---

## 👨‍💻 Author

**Mohamed Aziz Becheikh**

Full Stack Developer | Cloud & DevSecOps Enthusiast

GitHub: [@azizbh799-alt](https://github.com/azizbh799-alt)

---

## ⭐ Project

If you find this project useful, feel free to ⭐ the repository.
