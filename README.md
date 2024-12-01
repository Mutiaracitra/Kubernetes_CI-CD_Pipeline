# **Weekly Kubernetes CI/CD Pipeline Documentation**

## Introduction
This repository contains a fully automated CI/CD pipeline using Google Cloud Platform (GCP) services like Cloud Build, Docker, and Kubernetes Engine. The pipeline automates the process of building, pushing, and deploying a FastAPI application to Google Kubernetes Engine (GKE), utilizing load balancing for scalability.

## Project Structure
```
├── app/                          # Application code
├── kubernetes/                   # Kubernetes deployment and service configurations
│   ├── deployment.yaml           # Deployment configuration
│   ├── service.yaml              # Service configuration
├── Dockerfile                    # Dockerfile for application containerization
├── cloudbuild.yaml               # Cloud Build configuration for CI/CD pipeline
├── README.md                     # Project documentation
```

## Prerequisites
Before starting, ensure you have the following:
1. Google Cloud Platform (GCP) Account with billing enabled.
2. Google Cloud SDK installed.
3. kubectl installed for Kubernetes interaction.
4. Docker installed to build container images.

## Setup and Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/Mutiaracitra/weekly-kuberneets.git
cd weekly-kuberneets
```

### Step 2: Configure Cloud Build
Ensure your Google Cloud project and billing are set up. Use the Cloud Build configuration (`cloudbuild.yaml`) to automate the pipeline:
1. The pipeline builds the Docker image of the FastAPI app.
2. Pushes the Docker image to Google Container Registry.
3. Deploys the image to Google Kubernetes Engine (GKE).

### Step 3: Update Kubernetes Configurations
In the `kubernetes/` folder, modify the `deployment.yaml` and `service.yaml` files to suit your GKE setup, specifying the correct image name, replica count, and load balancing setup.

### Step 4: Deploy to GKE
Run the Cloud Build pipeline:
```bash
gcloud builds submit --config cloudbuild.yaml .
```
This triggers the pipeline, builds the app, pushes it to the registry, and deploys to GKE.

### Step 5: Accessing the Application
Once the deployment is complete, the FastAPI app is available through a load-balanced external IP. Use the following command to find the external IP:
```bash
kubectl get services
```
Access the application using the displayed external IP and port.

## CI/CD Pipeline Overview
The pipeline consists of three main stages:
1. Build: The Docker image of the FastAPI application is built.
2. Push: The Docker image is pushed to Google Container Registry.
3. Deploy: The image is deployed to Google Kubernetes Engine (GKE), making the application accessible through a LoadBalancer.

## Cloud Build Configuration
The `cloudbuild.yaml` file defines the steps:
- Step 1: Build the Docker image.
- Step 2: Push the image to GCR.
- Step 3: Authenticate to GKE and deploy the app.

