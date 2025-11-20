# Build Docker Image and Run container for a Simple Python web application #
**1) Project layout**
```   
   flask-docker/
    -app.py
    -requirements.txt
    -Dockerfile
```
**2) Create the app file (app.py)**

app.py — a tiny Flask app that returns Hello from Docker!
Paste the code into a file named app.py.

**3) Create requirements.txt**

This tells the image what Python packages to install. 
Create a file requirements.txt containing:
```
Flask==2.3.3
```
**4) Write the Dockerfile**

Create a file named Dockerfile and paste the code.

**5) Build the Docker image**

From the flask-docker folder (where Dockerfile is), run:
```
docker build -t my-flask-app:1.0 .
```
**6) Run the container**

Map the container’s port 5000 to your machine’s port 5000:
```
docker run --name my-flask -p 5000:5000 -d my-flask-app:1.0
```
**7) Open the app in your browser**
```
http://localhost:5000/
```
You should see: **Hello from Docker!**

**8) Push the image to Docker Hub**
```
# 1. Login
docker login

# 2. Tag local image
docker tag my-flask-app AishwaryaK001/my-flask-app:latest

# 3. Push to Docker Hub
docker push AishwaryaK001/my-flask-app:latest

# 4. Public repo link:
# https://hub.docker.com/r/AishwaryaK001/my-flask-app

# 5. you can pull/run:
docker pull AishwaryaK001/my-flask-app:latest
docker run -p 5000:5000 AishwaryaK001/my-flask-app:latest
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/3af6e086-114c-496b-85b8-6b4ff4cebe69" alt="AWS S3 Screenshot" width="600">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/f5f190a6-699b-40a8-8cfc-d199b93b01b9" alt="AWS S3 Screenshot" width="600">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/fe1305d9-2265-43cd-8f98-0bd0869c1a64" alt="AWS S3 Screenshot" width="600">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/8ead2e4e-353e-4506-9de3-f251e673acc4" alt="AWS S3 Screenshot" width="600">
</p>



