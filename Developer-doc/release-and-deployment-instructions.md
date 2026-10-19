# Release and Deployment Instructions

## Overview

CybergridML is deployed using Docker Compose. The deployment consists of two services:

* **db**: PostgreSQL 15 database
* **app**: CybergridML Spring Boot application

The application depends on the database being healthy before it starts.

## Prerequisites

Before deploying the application, make sure that the following tools are installed:

* Docker Engine
* Docker Compose
* Git

The deployment environment must also have access to the CybergridML source code.

## Configuration

Before starting the deployment, configure the required environment variables.

The following variables are used by the Docker Compose configuration:

```bash
POSTGRES_USER=<database_username>
POSTGRES_PASSWORD=<database_password>
POSTGRES_DB=<database_name>

DB_PORT=<database_port>
APP_PORT=<application_port>

POSTGRES_DATA_DIR=<path_to_postgres_data>
APP_DATA_DIR=<path_to_application_data>
```

These variables can be stored in a `.env` file located in the same directory as the `docker-compose.yml` file.

Example:

```bash
POSTGRES_USER=cybergrid
POSTGRES_PASSWORD=your_secure_password
POSTGRES_DB=cybergrid

DB_PORT=5432
APP_PORT=9090

POSTGRES_DATA_DIR=./postgres-data
APP_DATA_DIR=./app-data
```

> **Warning:** Sensitive information, such as database passwords, should not be committed to the Git repository.

## Deploying the Application

Clone the repository:

```bash
git clone https://github.com/cybergridml/cybergrid-models.git
cd cybergridmodel
```

Checkout the version to deploy:

```bash
git checkout vX.Y.Z
```

Replace `vX.Y.Z` with the version or release tag to deploy.

Start the application and the database:

```bash
docker compose up -d --build
```

Docker Compose will:

1. Build the CybergridML application image.
2. Start the PostgreSQL 15 database.
3. Wait for the database health check to succeed.
4. Start the CybergridML application.
5. Expose the application on the configured `APP_PORT`.

## Verifying the Deployment

Check that all containers are running:

```bash
docker compose ps
```

Check the application logs:

```bash
docker compose logs app
```

Check the database logs:

```bash
docker compose logs db
```

The application should be accessible on:

```text
http://<localhost>:<9090>
```

Verify that the application starts correctly and can connect to the PostgreSQL database.

## Updating the Application

To deploy a new version:

```bash
git pull
git checkout vX.Y.Z
docker compose down
docker compose up -d --build
```

Replace `vX.Y.Z` with the new release version.

## Stopping the Application

To stop the application and database containers:

```bash
docker compose down
```

The persistent volumes are not deleted when the containers are stopped, so the PostgreSQL database and application data are preserved.

## Rollback

If a deployment fails, redeploy the previous stable version.

```bash
docker compose down
git checkout vPREVIOUS_VERSION
docker compose up -d --build
```

After the rollback, verify that both containers are running correctly:

```bash
docker compose ps
```

Database compatibility should be checked before rolling back to an older application version.

[← Back to the main documentation](../README.md)