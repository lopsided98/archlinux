# Obsolete: replaced by https://github.com/lopsided98/archlinux-docker

# Basic Arch Linux images [![Build Status](https://travis-ci.org/lopsided98/archlinux.svg?branch=armv7h)](https://travis-ci.org/lopsided98/archlinux)

Docker images for Arch Linux on armv7h. Built daily by Travis CI on publicly visible infrastructure.

Based off of https://github.com/archimg/archlinux

## Running the images

The images are on [Docker Hub](https://hub.docker.com/u/lopsided/). Use the convenient `docker run`:

    docker run --rm -ti lopsided/archlinux-armv7h
    docker run --rm -ti lopsided/archlinux-armv7h:devel

## Tags

|  Tag   |  Update   |  Type   |                                                             Description                                                              |
|:------:|:---------:|:-------:|:-------------------------------------------------------------------------------------------------------------------------------------|
| latest | **daily** | minimal | most packages of base-group, except some big ones like [some big ones like `linux-firmware`](./Dockerfiles/basement/Dockerfile)      |
| full   | **daily** |   full  | all packages of base-group                                                                                                           |
| devel  | **daily** |   full  | all packages of base and base-devel-group                                                                                            |

### Layer structure

The image consists of two parts:

- the _[basement layer](./Dockerfiles/basement)_, derived from the tarball (updated monthly)
  - this layer has always its own tag in form of `YEAR.MONTH`
  - it's discouraged to use this as your base image
- the _[update layer](./Dockerfiles/updates)_, which only contains the updates (updated daily)
  - this layer has always its own tag as latest

This implies, that you get daily updates, but only have to download the actual change and not the full image.

## Issues and improvements

If you want to contribute, get to the [issues-section of this repository](https://github.com/lopsided98/archlinux/issues).

## Common hurdles

### Setting the timezone

Simply add the `TZ` environment-variable and define it with a valid timezone-value.

```
docker run -e TZ=Europe/Berlin archimg/base
```

## Building it yourself

### Prerequisites

- [docker-squash](https://github.com/goldmann/docker-squash/)
- sudo or root is absolutely neccessary to build the image from scratch
  - if you use `./pull` instead of `./build`, sudo is not required

### Building

- Run either `sudo -H ./build` **or** `./pull`
  - If you run `sudo -H ./build`, it'll download the tarball and build the images from scratch **(sudo required)**
  - If you run `./pull`, docker will download the images from dockerhub
- Run `./update` to generate the `latest`-tags and update the images.

If you want to push the images, run `./push`. *But be aware you have no push access to the repos!*
