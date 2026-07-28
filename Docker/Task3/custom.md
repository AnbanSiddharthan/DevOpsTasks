## Create a custom docker image for nginx and deploy it using docker compose, where the volume bind mount should be at /var/opt/nginx location. Push the created custom docker image to your docker-hub.

### Step 1: Create the Project

```bash
mkdir nginx-custom
cd nginx-custom
```
### Step 2: Create the Website Directory

```bash
sudo mkdir -p /var/opt/nginx
sudo chown -R $USER:$USER /var/opt/nginx
```

### Step 3: Create index.html

```bash
nano /var/opt/nginx/index.html
```
<img width="1472" height="746" alt="image" src="https://github.com/user-attachments/assets/306a8d28-1edb-4dab-bcef-a52aec285d83" />

### Step 4: Create Dockerfile

```bash
nano Dockerfile
```
<img width="1350" height="742" alt="image" src="https://github.com/user-attachments/assets/994c831d-6e61-4adf-b450-65689f61a847" />

### Step 5: Build the Image

```bash
docker build -t anbansiddharthan/custom-nginx:v1 .
```
### Step 6: Create docker-compose.yml

```bash
nano docker-compose.yml
```
<img width="1468" height="750" alt="image" src="https://github.com/user-attachments/assets/765299ff-3fcc-47aa-9049-06a75b0f05e7" />

### Step 7: Start

```bash
docker compose up -d
```
<img width="1917" height="972" alt="image" src="https://github.com/user-attachments/assets/965b2c33-4f87-4ad1-b64c-447148d3ce69" />

### Step 8: Test the Bind Mount

```bash
nano /var/opt/nginx/index.html
```
<img width="1466" height="751" alt="image" src="https://github.com/user-attachments/assets/8c220bc6-291e-4e79-92e7-7b2f044e0eee" />

### Step 9: Login to Docker Hub

```bash
docker login
```
<img width="1913" height="971" alt="image" src="https://github.com/user-attachments/assets/e1b02ee3-fb09-4a1f-9b68-521914326ffb" />

### Step 10: Push the Image

```bash
docker push anbansiddharthan/custom-nginx:v1
```
<img width="1917" height="902" alt="image" src="https://github.com/user-attachments/assets/31c96f2d-9043-4202-a802-5121040932f7" />

### Screenshots

<img width="1460" height="752" alt="image" src="https://github.com/user-attachments/assets/823efc92-1133-4f8c-b3e5-8dca7681b429" />

<img width="1917" height="1015" alt="image" src="https://github.com/user-attachments/assets/7521ddba-6f1e-4af2-9722-d21c9b8373f8" />

<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/3da7cfc7-3983-40a7-9c9e-1609e9450d92" />





