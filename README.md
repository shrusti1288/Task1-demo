# Task1-demo
Automate Code Deployment Using CI/CD Pipeline (GitHub Actions)

Step-by-Step CI/CD Setup

1. Project Structure (Example)

Your nodejs-demo-app should have:

nodejs-demo-app/
├── Dockerfile
├── .github/
│   └── workflows/
│       └── ci-cd.yml
├── package.json
├── app.js (or server.js)
└── ...

2. Dockerfile Example

# Use Node.js official image
FROM node:18

# Create app directory
WORKDIR /usr/src/app

# Copy package files and install
COPY package*.json ./
RUN npm install

# Copy rest of the app
COPY . .

# Expose port
EXPOSE 3000

# Run the app
CMD ["node", "app.js"]


3. GitHub Actions Workflow File: .github/workflows/ci-cd.yml

name: CI/CD Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Node.js
      uses: actions/setup-node@v4
      with:
        node-version: 18

    - name: Install dependencies
      run: npm install

    - name: Run tests (if you have any)
      run: npm test

    - name: Build Docker image
      run: docker build -t nodejs-demo-app .

    - name: Docker Hub Login
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Tag and Push Docker image
      run: |
        docker tag nodejs-demo-app ${{ secrets.DOCKER_USERNAME }}/nodejs-demo-app:latest
        docker push ${{ secrets.DOCKER_USERNAME }}/nodejs-demo-app:latest


4. Setup Secrets in GitHub

Go to your repository Settings > Secrets and variables > Actions > New repository secret and add:

DOCKER_USERNAME – Your Docker Hub username

DOCKER_PASSWORD – Your Docker Hub password or access token


5. Optional Deployment Targets

You can expand this to auto-deploy to services like:

Render

Heroku

AWS ECS

DigitalOcean App Platform

VPS (via SSH)





