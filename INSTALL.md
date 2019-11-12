# Install docker-ce / docker-compose / non-root on Debian 10
Todo: Some introduction

## 1. Install docker-ce

Login as the root user
```
su
```

Update the list of existing packages
```
apt update
```

Install required packages to allow apt over HTTPS
```
apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common
```

Add the Docker repository to the apt sources

```
curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
```

Update the package database with the Docker packages
```
apt update
```

Install Docker
```
apt install docker-ce
```

## 2. Allow non-root access to Docker

Create the docker group and add your user to it
```
/usr/sbin/groupadd docker
/usr/sbin/usermod -aG docker $USER
```
Log out and back in for the changes to be applied (or run `newgrp docker` from the user)

## 3. Install docker-compose

Download the (currently) stable version. https://github.com/docker/compose/releases
Run the following commands as the root user
```
curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
