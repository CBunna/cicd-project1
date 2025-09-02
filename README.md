# Task Manager App - CI/CD Pipeline

Simple Node.js task manager app with automated deployment.

## What's This?

A basic web app that gets automatically built and deployed when you push code to GitHub. No manual steps needed.

## Tools Used

- **GitHub Actions** - Builds Docker images when code changes
- **Docker** - Packages the app into containers  
- **Kubernetes** - Runs the app in containers (Local)
- **ArgoCD** - Watches for changes and updates deployments
- **GitHub Container Registry** - Stores Docker images

## How It Works

1. Push code to main branch
2. GitHub Actions runs automatically:
   - Tests the app
   - Builds Docker image with commit hash tag
   - Pushes image to registry
   - Updates deployment file with new image tag
3. ArgoCD sees the change in git
4. ArgoCD pulls new image and updates Kubernetes
5. App is live with your changes

## Local Setup

```bash
# Run locally
npm install
npm start
# App runs on http://localhost:3000
```

## Docker Commands

```bash
# Build image
docker build -t task-manager:v1.0.0 .

# Run container
docker run -p 3000:3000 task-manager:v1.0.0
```

## Kubernetes Files

- `k8s/deployment.yml` - Defines how app runs in Kubernetes
- Image tag gets updated automatically by CI/CD

## Pipeline Flow

```
Code Push → GitHub Actions → Docker Build → Registry Push → 
Git Update → ArgoCD Sync → Kubernetes Deploy → Live App
```

The image tag format: `ghcr.io/cbunna/cicd-project1:main-[commit-hash]`

## Health Check

App has `/health` endpoint that returns app status.

## Files Structure

- `app.js` - Main application file
- `Dockerfile` - Docker build instructions
- `.github/workflows/cicd.yml` - CI/CD pipeline
- `k8s/deployment.yml` - Kubernetes deployment config
- `public/` - Static files