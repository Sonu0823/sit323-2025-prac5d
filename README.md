# SIT323/SIT737: Cloud Native Application Development - Task 5.2D

## Overview

This task builds upon Task 5.1P and focuses on preparing a Dockerized Node.js microservice for production deployment by publishing the image to a private container registry hosted on **Google Cloud Artifact Registry (GCP)**. The objective is to verify that the image works when pulled from the cloud.

---

## Tools Required

Ensure the following tools are installed:

- **Git** – Version control
- **Visual Studio Code** – Code editor 
- **Node.js** – JavaScript runtime
- **Docker** – Container platform 
- **Google Cloud SDK** – GCP CLI tool 

---

### 1. Clone and Prepare the Project

Start by cloning your existing Task 5.1P repository:

git clone https://github.com/YOUR_USERNAME/sit323-2025-prac5p.git
mv sit323-2025-prac5p sit323-2025-prac5d
cd sit323-2025-prac5d 


### 2. Dockerize the Node.js Application

The Docker file uses a Node.js image, installs dependencies, copies source code, exposes port 8080, and starts the app using npm start.


### 3. Build and Run Locally

docker build -t my-node-app .
docker run -d -p 8080:8080 my-node-app

# Verify the app by visiting:

http://localhost:8080


### 4. Setup Google Artifact Registry

# Configure your GCP project:

gcloud config set project YOUR_PROJECT_ID
gcloud services enable artifactregistry.googleapis.com

Create the private registry.

### 5. Tag and Push the Docker Image

### Tag the image for your GCP Artifact Registry:

"docker tag my-node-app australia-southeast1-docker.pkg.dev/YOUR_PROJECT_ID/microservices-repo/my-node-app"

### Authenticate Docker with GCP:

gcloud auth configure-docker australia-southeast1-docker.pkg.dev

### Push the image:

docker push australia-southeast1-docker.pkg.dev/YOUR_PROJECT_ID/microservices-repo/my-node-app

### 6. Pull and Test the Cloud Image

To verify that the app works when pulled from the cloud:
docker run -d -p 8081:8080 australia-southeast1-docker.pkg.dev/YOUR_PROJECT_ID/microservices-repo/my-node-app

Test it on: http://localhost:8081

## Conclusion

This task demonstrated the full production pipeline: building, tagging, pushing, and running a cloud-hosted container image via Google Cloud Artifact Registry. 