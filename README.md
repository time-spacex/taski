## Overview

This is a simple project for creating notes. There are 2 tabs, when creating and editing, you can mark a note as completed. The project consists of three main parts:

+ Backend on Python with Django REST framework
+ Frontend on React
+ nginx gateway

The internal storage for the project is implemented on PostgreSQL 13.10.
CI/CD is implemented in /deploy/.gitlab-ci.yml

## CI/CD and infrastructure

To deploy a project on server via CI/CD commit your changes to master branch. This will launch a pipeline of 2 jobs: image (build and push images to Docker Hub) and deploy (copy and launch docker-compose.yml).

## How to install locally

At first check your system have docker
```
sudo docker info
```
Second - clone git repository
```
git clone git@gitlab-rkleshnev.ru:web/tasks.git
```
Third - create .env file with secrets for PostgreSQL in your /tasks folder:
```
# /tasks/.env

POSTGRES_USER=sample_user
POSTGRES_PASSWORD=sample_password
POSTGRES_DB=django
DB_HOST=db
DB_PORT=5432
```
Finally run docker-compose.yml to start the application.
```
sudo docker compose up -d
```
After all containers starts you need to compile static for django admin panel and make database maigartions, run these 2 commands in /tasks folder:
```
chmod +x ./collect_static.sh
./collect_static.sh
```
The locally running application will be available at http://localhost:8000

## System requirements

+ Linux Debian 12 or Ubuntu 22.04 or newer
+ Docker 26.1.4 or newer
