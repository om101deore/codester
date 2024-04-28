# Codester - A Dockerized Web Application

## Overview

Codester is a cloud computing project focused on demonstrating the use of Docker for efficient website deployment. By leveraging Docker containerization, this project showcases how a static website can be seamlessly packaged and deployed, highlighting Docker's simplicity and effectiveness in managing web applications. Accessible across multi-cloud platforms, Codester emphasizes scalability, portability, and ease of deployment. Powered by Docker, it exemplifies modern web development practices and infrastructure management strategies. Additionally, Codester serves as a product landing page, offering a user-friendly interface to showcase its features and offerings.

## Usage

### Prerequisites

- Docker installed on your system
- Dockerhub account 
- GitHub account

### Building the Docker Image

To build the Docker image, run the following command:

```bash
docker build -t om101deore/codester:latest .
```

### Running the Docker Container

To run the Docker container, execute:

```bash
docker run -d -p 5000:5000 your-image-name
```

### Accessing the Application

You can now access your application by navigating to `http://localhost:5000` in your web browser.

## Dockerfile

```Dockerfile
# Use the official Python image as a base image
FROM python:3.9

# Set the working directory in the container
WORKDIR /app

# Copy the requirements.txt file into the container at /app
COPY requirements.txt .

# Install Flask and other dependencies
RUN pip install -r requirements.txt

# Copy the current directory contents into the container at /app
COPY . .

# Expose port 5000 to the outside world
EXPOSE 5000

# Command to run the Flask application
CMD ["python", "app.py"]

```

## GitHub Actions

Create a `.github/workflows/main.yml` file with the following content:


```yaml
name: ci

on:
  push:
    branches:
      - "main"

jobs:
  docker:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v4

    - name: Set up QEMU
      uses: docker/setup-qemu-action@v3

    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v3

    - name: Login to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build and push
      uses: docker/build-push-action@v5
      with:
        context: .
        file: ./Dockerfile
        platforms: linux/amd64,linux/arm64
        push: true
        tags: |
          om101deore/codester:latest
          om101deore/codester:${{ github.run_number }}

```

Ensure you have set up the necessary secrets (`DOCKER_USERNAME` and `DOCKER_PASSWORD`) in your GitHub repository settings.

## Results
Webpage before changes
![Before Changes](https://github.com/om101deore/codester/blob/main/share/static_website.png)

Webpage after changing heading and pushing code to github
![After Changes](https://github.com/om101deore/codester/blob/main/share/changes_reflected.png)

Actions in use
![Actions in use](https://github.com/om101deore/codester/blob/main/share/actions.png)

Actions Successful
![Actions Successful](https://github.com/om101deore/codester/blob/main/share/actions_successful.png)

