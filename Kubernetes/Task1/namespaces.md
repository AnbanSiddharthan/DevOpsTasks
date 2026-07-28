## Setup minikube at your local and explore creating namespaces.

### Step 1: Start Minikube

```bash
minikube status
kubectl get nodes
```
<img width="1917" height="572" alt="image" src="https://github.com/user-attachments/assets/4948a5ed-fc65-4477-afbd-09c80b51b6d0" />

### Step 2: View Existing Namespaces

```bash
kubectl get namespaces
```
<img width="1915" height="405" alt="image" src="https://github.com/user-attachments/assets/f74096f0-410f-40d5-b016-f72923b065e9" />

### Step 3: Create a Namespace

```bash
kubectl create namespace dev
kubectl get ns
```
<img width="1907" height="772" alt="image" src="https://github.com/user-attachments/assets/d267ce7b-92f3-41bf-8329-503d32f1cf8c" />

### Step 4: Describe a Namespace


```bash
kubectl describe namespace dev
```
<img width="1240" height="237" alt="image" src="https://github.com/user-attachments/assets/f400c69d-2e51-4b45-84de-1500e72dcdeb" />

### Step 5: Create a Pod in a Namespace

```bash
kubectl run nginx \
  --image=nginx \
  --namespace=dev

kubectl get pods -n dev
```
<img width="1557" height="406" alt="image" src="https://github.com/user-attachments/assets/080cadbb-c953-4a19-a073-c748a456d1fb" />

### Step 6: Create a Pod in Another Namespace

```bash
kubectl run nginx-test \
  --image=nginx \
  --namespace=test
```
<img width="1906" height="666" alt="image" src="https://github.com/user-attachments/assets/746e0d07-fed4-4b63-9ff3-5f09f7a1389d" />


### Step 7: Change the Default Namespace


```bash
kubectl get pods -n dev
kubectl config set-context --current --namespace=dev
```
<img width="1415" height="338" alt="image" src="https://github.com/user-attachments/assets/31c27df2-c6c6-46e4-a164-df3efe38867d" />

### Step 8: Delete a Namespace

```bash
kubectl delete namespace test
```
<img width="1185" height="278" alt="image" src="https://github.com/user-attachments/assets/f3043d7f-2ecc-4112-ad90-2d24273329f8" />



