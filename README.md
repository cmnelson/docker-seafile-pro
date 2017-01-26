# Docker Image for Seafile 5 & 6 Pro Edition w/ nginx internal proxy

[![Docker Automated build](https://img.shields.io/docker/automated/cmnelson/docker-seafile-pro-nginx.svg)]()
[![Docker Stars](https://img.shields.io/docker/stars/cmnelson/docker-seafile-pro-nginx.svg)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/cmnelson/docker-seafile-pro-nginx.svg)]()
[![Docker Layers](https://images.microbadger.com/badges/version/cmnelson/docker-seafile-pro-nginx.svg)]()

## Introduction

This image will pull the latest pro edition of seafile and helps you set it up in a docker environment.

You'll be guided through the setup procedure. It's kept very basic.

Advanced configurations can be made directly via the configuration files generated during the setup.

## Setup

This will pull the latest image and start the setup process automatically. (interactive mode)
You'll be asked for some details (e.g. admin credentials).

```
docker run -it --rm \
	--name=seafile-setup \
	-v /var/seafile:/seafile \
	cmnelson/docker-seafile-pro-nginx setup
```

PLEASE NOTE THE "setup" FOLLOWING THE IMAGE NAME!

## Run

```
docker run -d \
	--name=seafile \
	-p 80:80 \
	-v /var/seafile:/seafile \
	cmnelson/docker-seafile-pro-nginx
```

## Upgrade (EXPERIMENTAL)

CAUTION: THIS FEATURE IS IN ITS CURRENT STATE EXPERIMENTAL. USE AT YOUR OWN RISK!

This image supports upgrading seafile too!

First, remove the seafile image. (You'll have to stop your container first)

```
docker stop seafile
docker rm seafile
docker rmi cmnelson/docker-seafile-pro-nginx
```

Proceed to run the container the same way you ran the setup. (except you'll need to use "upgrade" instead of "setup")

In our example you'll have to run the container by:

```
docker run -it --rm \
	--name=seafile-upgrade \
	-v /var/seafile:/seafile \
	cmnelson/docker-seafile-pro-nginx upgrade
```

This procedure requires a few minutes to complete. Please be patient and grab a coffee.

If for some reason seafile fails to start or you weren't patient, you can restore a backup of the state before seafile has been upgraded.
Backups are located at (in our example) `/var/seafile/backup` in .tar.gz format.
Start the container as usual after restoring the backup (see "Run").

## Contribute

This solution is quick'n'dirty, but works.
If you have any suggestions in order to improve this image, create a pull request/issue. Thank you!
