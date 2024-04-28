# Inherited Images Example

This project is a multi-stage Docker build setup with two services: build-base and build-app. The build-base service creates a base Docker image, and the build-app service uses this base image to create an application image. The project also includes a GitHub Actions workflow for building the Docker images.

## Project Structure

```yml
.github/
    workflows/
        build-app.yml
build-app/
    Dockerfile
    entrypoint-shim.sh
build-base/
    Dockerfile
    entrypoint-shim.sh
docker-compose.yml
```

- The build-base directory contains a Dockerfile and an entrypoint script for the base Docker image.
- The build-app directory contains a Dockerfile and an entrypoint script for the application Docker image.
- The docker-compose.yml file defines the services for building the Docker images.
- The .github/workflows/build-app.yml file is a GitHub Actions workflow for building the Docker images.

## Docker Images

The base Docker image is built from Alpine Linux and includes an environment variable MSG_BASE and MSG_BASE_OVERRIDE. The application Docker image is built from the base image and includes an additional environment variable MSG_APP.

The entrypoint script for each Docker image echoes the environment variables when the Docker container is run.

## GitHub Actions Workflow

The GitHub Actions workflow in build-app.yml builds the base Docker image, saves it as a Docker image artifact, and then uses this artifact to build the application Docker image.

## Running the Project

To build and run the Docker images, use the following command:

```bash
docker-compose up --build
```

This will build the Docker images and run the Docker containers. The entrypoint scripts will be executed, which will echo the values of the environment variables.

## What doesn't work

The GitHub Actions workflow is currently failing because the build-app service cannot find the base Docker image, even though it is saved as a Docker image artifact. I suspect that the issue is related to [upload-artifact action changing permissions](https://github.com/actions/upload-artifact/issues/38), but I haven't been able to confirm this. See any of the [failed workflow runs](https://github.com/ia-eknorr/test-build/actions) for more details.
