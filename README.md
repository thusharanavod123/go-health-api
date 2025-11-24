# go-health-api
The go-health-api project is a fundamental DevOps/Cloud-Native project we designed to demonstrate the full application lifecycle, from writing simple Go code to deploying it as a containe
Here is the complete README.md file for your Go Health Check API project, structured professionally and ready to be used on GitHub.

It emphasizes the DevOps and Cloud-Native aspects of the project, highlighting the CI/CD pipeline you built.

🛠️ Go Health API: Cloud-Native CI/CD Project
This repository hosts a simple, high-performance Go REST API server designed specifically for demonstration and deployment within containerized environments (like Docker and Kubernetes).

Its primary function is to provide a reliable health check endpoint, making it an ideal candidate for integration into automated Continuous Integration/Continuous Deployment (CI/CD) pipelines.

✨ Project Features
Fast & Lightweight: Built entirely in Go (Golang), resulting in a single, static binary for minimal overhead and maximum performance.

Health Endpoint: Exposes a standard /health endpoint for readiness/liveness probes by orchestrators.

Containerized: Includes a robust Dockerfile utilizing a multi-stage build for minimal image size (~10MB final size).

Automated CI/CD: Integrated with GitHub Actions to automatically build, tag, and push the Docker image to Docker Hub upon code changes

Layer,Technology,Role in the Project
Backend,Go (Golang),Provides the highly performant and concurrent API server (net/http).
Containerization,Docker,Packages the application and its dependencies for consistent deployment.
Automation,GitHub Actions,"Orchestrates the build, login, tagging, and push phases of the CI/CD pipeline."
Registry,Docker Hub,"Stores the final, versioned container images."

🚀 Getting Started
Prerequisites
You must have the following installed on your local machine:

Go (version 1.20+)

Git

Docker Desktop (or Docker Engine)

1. Local Setup
Clone the repository and run the application locally:

Bash

# Clone the repository
git clone [YOUR_REPO_URL]
cd go-health-api

# Run the Go server directly
go run cmd/api/main.go
# Server starting on port :8080...
2. Local Verification (API Check)
With the server running (in a separate terminal window), verify the health endpoint using curl:

Bash

curl http://localhost:8080/health
Expected Output:

JSON

{"status": "UP", "message": "Service is healthy and running."}
🐳 Deployment (The DevOps Cycle)
1. Manual Docker Build
Build the final production image using the multi-stage Dockerfile:

Bash

# Build the image and tag it
docker build -t go-health-api-local:latest .
2. Run the Container
Run the newly built image, mapping the container's internal port 8080 to your local machine's port 8080:

Bash

docker run -d -p 8080:8080 --name health-service go-health-api-local:latest
3. CI/CD Automation
This project is configured for automated deployment via GitHub Actions.

Trigger: Any push to the main or develop branch automatically starts the workflow.

Configuration: The CI/CD logic is defined in .github/workflows/docker-build-push.yml.

Required GitHub Secrets: To allow the pipeline to push the image, you must define the following secrets in your repository settings

Secret Name,Value,Purpose
DOCKER_USERNAME,Your Docker Hub Username.,Authentication for the registry.
DOCKER_PASSWORD,Your Docker Hub Access Token.,Secure credential for pushing images.