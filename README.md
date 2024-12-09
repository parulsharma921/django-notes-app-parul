

# Django Notes App Deployment on AWS EC2 using Docker

This repository demonstrates how to deploy a Django Notes App on an AWS EC2 instance using Docker for containerization. Below are the steps to set up and run the application.

## Prerequisites
- AWS EC2 instance (Ubuntu)
- Docker installed
- Git installed

---

## Steps to Deploy

### 1. Update and Install Docker
Update the system packages and install Docker:
```bash
sudo apt-get update
sudo apt-get install docker.io
```

### 2. Configure Docker
Add your user to the Docker group to avoid using `sudo` for Docker commands:
```bash
sudo usermod -aG docker ubuntu
```
**Note**: Log out and log back in for the changes to take effect.

If Docker still requires `sudo`, change the ownership of the Docker socket:
```bash
sudo chown ubuntu /var/run/docker.sock
```

Verify Docker installation:
```bash
docker ps
```

---

### 3. Clone the Repository
Clone the project from GitHub:
```bash
git clone https://github.com/parulsharma921/django-notes-app-parul.git
```

Navigate to the project directory:
```bash
cd django-notes-app-parul
```

---

### 4. Create and Configure Dockerfile
If you need to recreate the `Dockerfile`, follow these steps:
1. Remove the existing `Dockerfile`:
   ```bash
   rm Dockerfile
   ```
2. Create a new `Dockerfile`:
   ```bash
   vim Dockerfile
   ```
3. Add the following content to your `Dockerfile`:
   ```dockerfile
   FROM python:3.8-slim

   # Set the working directory
   WORKDIR /app

   # Copy the application files
   COPY . /app

   # Install dependencies
   RUN pip install -r requirements.txt

   # Expose the application port
   EXPOSE 8000

   # Command to run the application
   CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
   ```

Save and exit the editor.

---

### 5. Build the Docker Image
Build the Docker image for the Django Notes App:
```bash
docker build -t django-notes-app .
```

---

### 6. Run the Application
Run the container and expose port 8000:
```bash
docker run -p 8000:8000 django-notes-app
```

Access the app in your browser using the public IP of your EC2 instance and port 8000:
```
http://<YOUR_EC2_PUBLIC_IP>:8000
```

---

## Notes
- Make sure port 8000 is allowed in the EC2 security group.
- Use `docker ps` to verify that the container is running.

---

## Project Features
- **Backend**: Django framework.
- **Containerization**: Dockerized for seamless deployment.
- **Cloud Hosting**: Deployed on AWS EC2.

---

## Troubleshooting
- If the app doesn’t run, check the Docker logs:
  ```bash
  docker logs <CONTAINER_ID>
  ```
- Verify Dockerfile syntax and dependencies in `requirements.txt`.

---


