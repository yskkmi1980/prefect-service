# Prefect running on docker

## Summary

Place configuration files, etc. to build the Prefect environment that runs on the docker.

## Module

```
├── README.md # Markdown file of this document
├── server.yml # Server core docker-compose file
├── ui.yml # UI docker-compose file
└── service
    ├── prefect-server.service # 
    └── prefect-ui.service
```

## Installation

Docker and docker-compose must be installed by each user.

Create a user to launch the application container

```sh
$ sudo adduser prefect --disabled-password
$ sudo gpasswd -a prefect docker
```

Obtain sources and deploy systemd service files

```sh
$ sudo su - root
$ cd /opt && git clone <this module git repository url> && chown -rf prefect:prefect prefect-service && cd prefect-service
$ cp service/prefect-server.service /etc/systemd/system/
$ cp service/prefect-ui.service /etc/systemd/system/
```

Register prefect-server service to systemd and start service

```sh
$ sudo systemctl enable --now prefect-server.service
$ sudo systemctl start prefect-server.service
```

http://localhost:8080/