## Create a dockerfile, docker-compose file which when executed must display your basic details in the website.

### Create a Project Folder
```bash
mkdir docker-profile
cd docker-profile
```
### Create the HTML Page
```bash
nano index.html
```
<img width="1455" height="741" alt="image" src="https://github.com/user-attachments/assets/61a664d8-98fd-4658-b04a-5e1ac1e8511c" />

### Create the Dockerfile
```bash
nano Dockerfile
```
<img width="1473" height="757" alt="image" src="https://github.com/user-attachments/assets/c83a435d-555b-4bbe-ab35-bc3a7d89f199" />

### Build the Image
```bash
docker build -t myprofile:v1 .
```
<img width="1481" height="748" alt="image" src="https://github.com/user-attachments/assets/fe199e56-251f-4ca0-a8b6-98567f00364f" />

### Create docker-compose.yml
```bash
nano docker-compose.yml
```
<img width="1470" height="752" alt="image" src="https://github.com/user-attachments/assets/f5c71b4b-eec8-4a58-b485-c273945de2f7" />

### Run Using Docker Compose
```bash
docker compose up -d
docker ps
```
<img width="1916" height="957" alt="image" src="https://github.com/user-attachments/assets/d27f2e63-6120-4d64-9dd1-21ee864b7a11" />


