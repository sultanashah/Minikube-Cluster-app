DevOps Internship

# 🚀 Task 5: 

# Build a Kubernetes Cluster Locally with Minikube

## 🎯 Objective
Deploy and manage applications in a Kubernetes cluster using Minikube, kubectl, and Docker.
---

## 🧰 Tools Used
- Minikube
- kubectl
- Docker
- AWS EC2 (Ubuntu 24.04)
- Git Bash (for SSH with port forwarding)

---

## 📦 Setup Steps

### 1. ✅ Minikube & Docker Installation (on EC2)
```bash
sudo apt update
sudo apt install -y docker.io conntrack curl
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### 2. 🔥 Start Minikube
```bash
minikube start --driver=docker
```

---

## 📟 Deployment Files

### 📄 `deployment.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```

### 📄 `service.yaml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```

---

## 🚀 Deployment Commands

### Apply Deployment & Service:
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Verify Pods & Services:
```bash
kubectl get pods
kubectl get services
```

### Scale the Deployment:
```bash
kubectl scale deployment my-nginx --replicas=4
```

### Inspect Details & Logs:
```bash
kubectl describe deployment my-nginx
kubectl logs <pod-name>
```

---

## 🌐 Access the App from Browser

### From Local Machine:
Forward port from EC2 → local machine:
```bash
ssh -i /c/Users/User/Downloads/minikube-key.pem -L 8080:localhost:8080 ubuntu@<EC2-PUBLIC-IP>
```

Then in EC2:
```bash
kubectl port-forward service/nginx-service 8080:80
```

Open your browser and go to:
```
http://localhost:8080
```

---

## 📸 Screenshots to Include (Deliverables)

- `kubectl get pods`
- `kubectl get services`
- `kubectl describe deployment my-nginx`
- Web page in browser (localhost:8080 showing NGINX)

---

## ✅ Summary

In this task, we:
- Installed Minikube on an EC2 Ubuntu instance
- Created a Kubernetes deployment and exposed it via a service
- Scaled the app using `kubectl scale`
- Verified everything using `kubectl` commands
- Accessed the app locally via port forwarding

---

