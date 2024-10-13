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

## Monitoring

For monitor the application and other docker based services check link:
http://194.67.88.232/monitoring/d/ee0qt1ul66m80b/docker-monitoring?orgId=1&refresh=10s

Alert rules you can check to this link:
http://194.67.88.232/monitoring/alerting/list

There are several tools implemented on the server:

+ Grafana - latest release for visual representation of the status of services and applications;
+ Prometheus - latest release for scrape metrics;
+ Cadvisor:canary - collects metrics from application and monitoring services;
+ Loki:2.8.0 - for collecting logs and translate to grafana;
+ Fluentd - as a plugin for grafana/loki service to collect logs from containers.

These tools are collected in a separate project, you can check the link for a details: http://gitlab-rkleshnev.ru/web/tasks-monitoring

### Project authors

Application backend, infrastructure and CI/CD made by Kleshnev Roman (teleghram - @metandr, GitHub - time-spacex)
frontend made by Yandex.Practicum

2024 Oct