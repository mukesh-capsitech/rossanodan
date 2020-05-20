---
title: "How to create a personal photo server"
date: 2020-05-16
draft: false
categories: [ General ]
tags: [ raspberrypi nextcloud docker ]
featuredImage: ""
featuredImagePreview: ""
---

I do like travelling and taking pictures, even if most of them are really pointless :smile:

Once back at home, I'm used to move all the pictures I took on my laptop and, after a selection, I upload the best pictures to the cloud. I like using Google Photos. But there's a problem.
Since I use the Free plan, I don't upload pictures with the original size. It means they lose quality.

That's why I decided to buy an HDD and to upload my pictures on it, not using Google Photos anymore.

Damn I miss it.

I don't have access to my pictures anymore when I'm not around my HDD. Showing and/or sharing them's impossible.

That's when the idea of the private cloud started floating in my mind.

You may say buying a HDD wasn't a cost? Pay for Google Photos then! You're right but nothing is better than the satisfaction you get by something built by yourself. I really like doing this kind of things so I made my private Google Photos! It's a full private cloud service actually - documents, video, images, emails, etc - but I use it only for my pictures.

## Prerequisites

### Raspberry Pi and Micro SD

To setup my photo server I used a Raspberry Pi 4 (4 GB RAM) with 16 GB Micro SD and an external USB drive to use as storage.

![Installing Raspbian on the Micro SD](/images/installing_raspbian.png)

### Docker and Docker Compose

I also installed Docker on my Raspberry Pi: I didn't want to re-install everything in case something goes wrong.

Once installed, I did make sure the user `pi` can use it (I don't want to use `sudo` every time)

```
curl -fsSl https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker pi
```

and then I checked the installation

```
docker version
Client: Docker Engine - Community
 Version:           19.03.8
 API version:       1.40
 Go version:        go1.12.17
 Git commit:        afacb8b
 Built:             Wed Mar 11 01:35:24 2020
 OS/Arch:           linux/arm
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.8
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.17
  Git commit:       afacb8b
  Built:            Wed Mar 11 01:29:22 2020
  OS/Arch:          linux/arm
  Experimental:     false
 containerd:
  Version:          1.2.13
  GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
```

I installed Docker Compose too - kudos to [Roahn](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl) for the help

```
sudo apt-get install -y libffi-dev libssl-dev python3 python3-pip
sudo apt-get remove python-configparser
sudo pip3 install docker-compose

docker-compose --version
docker-compose version 1.25.5, build unknown
```

Since the architecture of the Raspberry Pi is different than the classic Ubuntu's, I needed to install Docker Compose via `pip3`.

## Declare the infrastructure

To setup Nextcloud I used a `yml` file `docker-compose.yml`

```
version: '2'

volumes:
  nextcloud:

services:
  app:
    image: nextcloud
    ports:
      - 8080:80
    volumes:
      - nextcloud:/var/www/html
    restart: always
```

This `yml` file contains the infrastructure I want to build. This way to build infrastructures is called **IaC**, Infrastructure as Code: you declare the services you want to run and how they have to communicate each other and Docker Compose does the job for you.

## Up and running

Now that the `docker-compose.yml` is ready, it's time to launch!

```
docker-compose up -d
```

The option `-d` stands for `detached mode`, containers run in background.

To check if the container we declared in the `yml` file is up and running, run

```
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
a1d31d5ee1d6        nextcloud           "/entrypoint.sh apac…"   About an hour ago   Up About a minute   0.0.0.0:8080->80/tcp   nextcloud_app_1
```

I can do something similar with Docker Compose. Within the root folder  that contains the `docker-componse.yml` file, run

```
docker-compose ps
     Name                    Command               State          Ports
-------------------------------------------------------------------------------
nextcloud_app_1   /entrypoint.sh apache2-for ...   Up      0.0.0.0:8080->80/tcp
```

The difference between `docker ps` and `docker-compose ps` is that `docker ps` lists all running containers in docker engine while `docker-compose ps` lists containers related to images declared in the `docker-compose.yml` file.
