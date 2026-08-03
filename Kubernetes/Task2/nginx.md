## Create the K8s EKS,further you have to do the deployment of the Nginx application and access the application outside the cluster.

### 1. Update the system

```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Install AWS CLI

```bash
sudo apt install awscli -y
aws --version
```

### 3. Install kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x kubectl

sudo mv kubectl /usr/local/bin/
```

### 4. Install eksctl

```bash
curl --silent --location \
"https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" \
| tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin
```

### 5. Configure AWS

```bash
aws configure
aws sts get-caller-identity
```

### 6. Create the EKS Cluster

```bash
eksctl create cluster \
  --name my-eks-cluster \
  --region eu-north-1 \
  --nodegroup-name workers \
  --node-type t3.micro \
  --nodes 2
```

### 7. Deploy Nginx

```bash
kubectl create deployment nginx --image=nginx
kubectl get pods
```

### 8. Expose Nginx

```bash
kubectl expose deployment nginx \
  --type=LoadBalancer \
  --port=80 \
  --target-port=80
```

### 9. Get the Load Balancer Address


```bash
kubectl get svc
```
### Screenshots

<img width="1917" height="1006" alt="image" src="https://github.com/user-attachments/assets/7aee3b51-2371-4bf4-8b20-511f65907a50" />

<img width="1917" height="950" alt="image" src="https://github.com/user-attachments/assets/c71453ca-114e-4441-8733-0a1c18f58972" />

<img width="1917" height="1020" alt="image" src="https://github.com/user-attachments/assets/87a381eb-0480-48d7-aa84-f9589c8c0c76" />

<img width="1917" height="943" alt="image" src="https://github.com/user-attachments/assets/45f13d69-d9c9-4594-b141-77733d9781e6" />

<img width="1917" height="1010" alt="image" src="https://github.com/user-attachments/assets/670fd4d4-d134-406a-9239-0300dd61dd62" />

<img width="1917" height="971" alt="image" src="https://github.com/user-attachments/assets/e20f2206-3e22-4ffd-a5e1-a27cf35bb19c" />

<img width="1917" height="922" alt="image" src="https://github.com/user-attachments/assets/dfc43cfc-ffb1-436b-bb17-e9c8a398b6bd" />

<img width="1917" height="965" alt="image" src="https://github.com/user-attachments/assets/ecf117d3-58fb-4f69-86ae-282ad9cf2bd5" />
