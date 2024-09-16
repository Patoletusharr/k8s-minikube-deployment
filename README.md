# Deploy Your First Application on Kubernetes cluster using Minikube 

This repository contains a step-by-step guide for setting up a Kubernetes cluster using Minikube and Docker as the driver on an EC2 instance. We'll deploy an Nginx application as an example.

---

## Step 1: Prerequisites

Before you begin, make sure you have the following:
- **AWS EC2 instance**: Ubuntu 22.04 LTS (or later) with at least 2 vCPUs (e.g., t2.medium or t3.medium).
- **Security Group**: Open port 22 (SSH) and port 80 (HTTP) in your EC2 security group.
- Basic knowledge of **Docker** and **Kubernetes**.


## Step 2: Install Required Software

2.1 Update your instance and install `curl`:

```bash
sudo apt update
sudo apt install curl -y

```

2.2 Download and install the Kubernetes CLI tool (kubectl):

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client

```
2.3 Download and install Minikube:

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

```
2.4 Install Docker and configure it:

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker

```
2.5 Add your user to the Docker group to manage Docker without sudo:
```bash
sudo usermod -aG docker $USER
newgrp docker

```

2.5 Start Minikube with Docker as the driver

```bash
minikube start --driver=docker

```
# Step 3:  Deploy Your First Applicationer

- 3.1 Create a file named pod.yaml with the following content:

  ```bash
    vi pod.yaml
```

```bash
    apiVersion: v1
    kind: Pod
    metadata:
     name: nginx
    spec:
    containers:
    - name: nginx
      image: nginx:1.14.2
      ports:
       - containerPort: 80


```

- 3.2 Run the following command to deploy the Nginx pod:
```bash
kubectl apply -f pod.yaml

```

- 3.3 Expose the Nginx pod to be accessible from outside:
```bash
kubectl expose pod nginx --type=NodePort --port=80

```
- 3.4 Check the service details:
```bash
kubectl get services

```
- 3.5 Get the URL to access your Nginx service:

```bash

minikube service nginx --url

```
Open the URL in your browser, and you should see the Nginx welcome page.


# Step 5: Cleaning Up

- Once you're done, you can stop Minikube:
```bash

miniKube stop 

```

- If you want to delete the resources (Pod and Service):


```bash

kubectl delete pod nginx
kubectl delete service nginx

```




## Step 2: Install Required Software

2.1 Update your instance and install `curl`:

```bash
sudo apt update
sudo apt install curl -y

```

2.2 Download and install the Kubernetes CLI tool (kubectl):

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client

```
2.3 Download and install Minikube:

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

```
2.4 Install Docker and configure it:

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker

```
2.5 Add your user to the Docker group to manage Docker without sudo:
```bash
sudo usermod -aG docker $USER
newgrp docker

```

2.5 Start Minikube with Docker as the driver

```bash
minikube start --driver=docker

```
# Step 3:  Deploy Your First Applicationer

- 3.1 Create a file named pod.yaml with the following content:

  ```bash
    vi pod.yaml
```

```bash
    apiVersion: v1
    kind: Pod
    metadata:
     name: nginx
    spec:
    containers:
    - name: nginx
      image: nginx:1.14.2
      ports:
       - containerPort: 80


```

- 3.2 Run the following command to deploy the Nginx pod:
```bash
kubectl apply -f pod.yaml

```

- 3.3 Expose the Nginx pod to be accessible from outside:
```bash
kubectl expose pod nginx --type=NodePort --port=80

```
- 3.4 Check the service details:
```bash
kubectl get services

```
- 3.5 Get the URL to access your Nginx service:

```bash

minikube service nginx --url

```
Open the URL in your browser, and you should see the Nginx welcome page.


# Step 5: Cleaning Up

- Once you're done, you can stop Minikube:
```bash

miniKube stop 

```

- If you want to delete the resources (Pod and Service):


```bash

kubectl delete pod nginx
kubectl delete service nginx

```




## Lessons Learned

This guide shows how to deploy an Nginx app using Kubernetes with Minikube and Docker on an AWS EC2 instance. Feel free to clone this repository, follow the instructions, and explore further Kubernetes use cases.
