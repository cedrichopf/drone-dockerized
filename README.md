# Drone Dockerized

- [Drone Dockerized](#drone-dockerized)
  - [Overview](#overview)
  - [Requirements](#requirements)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)

---

## Overview

This repository contains a template to deploy [Drone CI](https://drone.io/) using [Docker Compose](https://docs.docker.com/compose/) on a single machine running [Docker](https://www.docker.com/).

## Requirements

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Git](https://git-scm.com/)
- Text editor of your choice (e.g. [Vim](https://www.vim.org/))

## Installation

Clone the repository:

```sh
$ git clone https://github.com/cedrichopf/drone-dockerized.git
Cloning into 'drone-dockerized'...
```

Create a copy of the example configuration files:

```sh
# Drone Configuration
$ cp example.env .env
# Custom Docker Compose Configuration
$ cp override.example.yml docker-compose.override.yml
```

Configure the Drone deployment by adapting the environment variables in the `.env` file:

```sh
$ vim drone.env
```

Further information about the available environment variables can be found here: [Environment Variables](#environment-variables)

Configure the docker-compose.override.yml file:

```sh
$ vim docker-compose.override.yml
```

**Important:** The example configuration doesn't publish any ports by default. It uses an existing [Traefik](https://containo.us/traefik/) instance as a reverse proxy to access the Drone instance. If you want to publish ports, please add them to the `docker-compose.override.yml` configuration.

Download the Docker images and start the services using docker-compose:

```sh
$ docker-compose pull
$ docker-compose up -d
```

Open your browser and access your Drone instance using the URL of the Docker host and the configured route, e.g. [http://127.0.0.1](http://127.0.0.1).

## Environment Variables

The following table contains an overview of the environment variables which can be configured in the `drone.env` file. Further information about the available environment variables can be found here: [Drone Server Reference](https://docs.drone.io/server/reference/)

**Important:** If you want to add environment variables which are not listed below (e.g. BitBucket configuration), you need to add them to the `drone.env` and `docker-compose.override.yml` file.

| Environment Variable       | Example                                             | Description                     |
| -------------------------- | --------------------------------------------------- | ------------------------------- |
| COMPOSE_PROJECT_NAME       | `drone`                                             | Project name for docker-compose |
| DRONE_AGENTS_ENABLED       | `true`                                              | Use agents to run pipelines     |
| DRONE_GIT_ALWAYS_AUTH      | `true`                                              | Git server requires login       |
| DRONE_GITEA_CLIENT_ID      | `bea26a2221fd8090ea38720fc445eca6`                  | OAuth Client ID for Gitea       |
| DRONE_GITEA_CLIENT_SECRET  | `bea26a2221fd8090ea38720fc445eca6`                  | OAuth Client Secret for Gitea   |
| DRONE_GITEA_SERVER         | `https://try.gitea.io`                              | Gitea Server Endpoint           |
| DRONE_GITHUB_CLIENT_ID     | `bea26a2221fd8090ea38720fc445eca6`                  | OAuth Client ID for GitHub      |
| DRONE_GITHUB_CLIENT_SECRET | `bea26a2221fd8090ea38720fc445eca6`                  | OAuth Client Secret for GitHub  |
| DRONE_RPC_SECRET           | `bea26a2221fd8090ea38720fc445eca6`                  | Drone RPC Secret                |
| DRONE_SERVER_HOST          | `drone.example.com`                                 | Hostname of the Drone CI Server |
| DRONE_SERVER_PROTO         | `https`                                             | Protocol (http/https)           |
| DRONE_USER_CREATE          | `username:octocat,admin:true`                       | Administrator setup             |
| DRONE_USER_FILTER          | `octocat,spaceghost`                                | User filter                     |
| DRONE_DATABASE_DRIVER      | `postgres`                                          | Database type                   |
| DRONE_DATABASE_DATASOURCE  | `postgres://drone:<password>@postgresql:5432/drone` | Database connection string      |
| DRONE_DATABASE_SECRET      | `some-secret`                                       | Database secret                 |
| DRONE_S3_ENDPOINT          | `https://play.min.io`                               | S3 Endpoint                     |
| DRONE_S3_PATH_STYLE        | `false`                                             | S3 Path Style                   |
| DRONE_S3_BUCKET            | `my-bucket`                                         | S3 Bucket Name                  |
| DRONE_S3_PREFIX            | `some/path`                                         | S3 Prefix                       |
| DRONE_S3_SKIP_VERIFY       | `true`                                              | Skip S3 SSL Certificate         |
| AWS_ACCESS_KEY_ID          | `aws-access-key`                                    | AWS Access Key                  |
| AWS_SECRET_ACCESS_KEY      | `aws-secret-key`                                    | AWS Secret Key                  |
| AWS_DEFAULT_REGION         | `eu-central-1`                                      | AWS Default Region              |
| AWS_REGION                 | `eu-central-1`                                      | AWS Region                      |
| POSTGRES_USER              | `drone`                                             | PostgreSQL Username             |
| POSTGRES_PASSWORD          | `drone-db-password`                                 | PostgreSQL Password             |
| POSTGRES_DB                | `drone`                                             | PostgreSQL Database Name        |
