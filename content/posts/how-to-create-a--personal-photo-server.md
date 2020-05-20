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

I also installed [Docker](https://www.docker.com/) on my Raspberry Pi: I didn't want to re-install everything in case something goes wrong.

Once installed, I did make sure the user `pi` can use it (I don't want to use `sudo` every time)

```
curl -fsSl https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker pi
```

and then I checked the installation

```
docker --version
Docker version 19.03.8, build afacb8b
```

I installed [Docker Compose](https://docs.docker.com/compose/) too - kudos to [Roahn](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl) for the help

```
sudo apt-get install -y libffi-dev libssl-dev python3 python3-pip
sudo apt-get remove python-configparser
sudo pip3 install docker-compose

docker-compose --version
docker-compose version 1.25.5, build unknown
```

Since the architecture of the Raspberry Pi is different than the classic Ubuntu's, I needed to install Docker Compose via `pip3`.

## Declare the infrastructure

To setup [Nextcloud](https://nextcloud.com/) I used a `yml` file `docker-compose.yml`

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

In this case, I declared I want to use the [`nextcloud` image](https://hub.docker.com/_/nextcloud/) to run an app on the port `8080` (or `80` if the `8080` is busy). I also specified the path for the `volume` - where the container stores data (my photos).

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

If you're on your Raspberry, go to `http://localhost:8080/`. If you're connected to the Raspberry Pi via SSH instead, open a browser and go to `http://[HOSTNAME]:8080/`. 

> If you don't know the IP address of your Raspberry Pi, just run
>
> ```
> hostname -I
> 192.168.1.162 172.17.0.1 172.29.0.1 169.254.70.85 172.21.0.1 169.254.52.242 2a00:23c7:8e8b:1201:f35:95a7:4c14:6ed
> ```
>
> So, in my case, my Raspberry's IP address is `192.168.1.162`. It shouldn't change until you disconnect the Raspberry from the Internet > or you restart the router.

Here's [a good article](https://itsfoss.com/ssh-into-raspberry/) about how to connect via SSH to your Raspberry Pi.

Ta-da! Nextcloud is up and running, ready to be initialized!

## Let's take a closer look

Sweet, Nextcloud is working and is reachable only within my WiFi connection. I can upload photos from my smartphone too!

Let's take a look at the container. Run

```
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
a1d31d5ee1d6        nextcloud           "/entrypoint.sh apac…"   2 hours ago         Up 37 minutes       0.0.0.0:8080->80/tcp   nextcloud_app_1
```

and copy the container id. Now run

```
docker exec -it <CONTAINER_ID> bash
```

to enter the container itself, in interactive mode (`-it`).
