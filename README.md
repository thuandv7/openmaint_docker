# openmaint_docker

### What is openMAINT?

openMAINT is web based Property & Facility Management application that is fully open source. It is used for managing fixed and transferable physical assets such as buildings and furniture, along with related maintenance.

### What stack does this distro of openMAINT use?

This is a fully functional OpenMAINT 2.0 solution using docker containers that employs the following customized stack:

- CMDBuild 3.1.1 core
- OpenMAINT 2.0 database dump
- Tomcat 8.5.42
- OpenJDK version 1.8.0_212
- PostgreSQL 10.7
- Debian 9.9 (stretch)

### What is CMDBuild?

CMDBuild is an open source asset management application that OpenMAINT is built upon. Except for some differences in the database, they are virtually identical and share the same code base.

### Docker & Docker Compose

Docker is a popular tool that makes it easy to create, deploy, and run applications using containers. Containers allow developers to package and ship an application with a full stack of dependencies it needs to run on any other system, regardless of any conflicting configurations that may be present. Docker Compose is a companion tool for creating and running multi-container docker applications.

openmaint_docker was built and tested using the following Docker tools:

- Docker-Compose version 1.21.2, build a133471
- Docker version 19.03.5, build 633a0ea838
- Docker Pull: mrhavens/cmdbuild:app-3.1.1 (Docker Hub Repo)
- Docker Pull: mrhavens/cmdbuild:db-3.0 (Docker Hub Repo)

# Installation Instructions for Ubuntu 18.04 LTS

### Update APT Repository 
```
sudo apt update
```

### Install Docker
```
sudo apt -y install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt -y install docker-ce
```

### Install Docker Compose
```
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### Build Tomcat & PostgreSQL Containers
```
git clone https://github.com/mrhavens/openmaint_docker.git
cd openmaint_docker
```

Build and bring up the database container.
```
docker-compose up -d openmaint_db
```

Wait between three to five minutes for the database to come fully online, then build and bring up the Tomcat container. If you bring the Tomcat container up too early, it will terminate, and you will have to restart it again.
```
docker-compose up -d openmaint_app
```

# Administration

OpenMAINT defaults to the following URL:

```
http://<openmaint_ip-address>:8080/cmdbuild
```
Where <openmaint_ip-address> is the IP address or fully qualified domain name of the server with OpenMAINT installed.

If your server is behind a firewall that doesn't have ports 8080 open, you can redirect all traffic through an ssh tunnel that targets your unrestricted localhost:

```
ssh -L 8080:localhost:8080 root@<openmaint_ip-address>
```

And then browse to the following URL:

```
http://localhost:8080/cmdbuild
```

Defaut admin credentials to log into OpenMAINT are:

```
OpenMAINT Admin Username: admin
OpenMAINT Admin Password: admin
```

Default admin credentials to log into Tomcat admin console are:
```
Tomcat Admin Username: admin
Tomcat Admin Password: password
```
