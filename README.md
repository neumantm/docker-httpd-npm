# docker-httpd-npm
[![Docker](http://dockeri.co/image/neumantm/httpd-npm)](https://hub.docker.com/r/neumantm/httpd-npm/)

This repository contains some Dockerfiles for Apache [HTTPD](https://httpd.apache.org/) containers, 
which include [node.js](https://nodejs.org/) and the [npm](https://www.npmjs.com/), the node package manager.

This is thought as a base container for applictaions that need npm and should be served by apache HTTPD.

All files use [httpd](https://hub.docker.com/_/httpd/) as their base image and install npm on top of that.

Currently only the alpine variant of http is supported.

## Buildinging
The Dockerfile uses build arguments to determine the versions of the used software.
To build your own image with specific versions use

    docker build . --build-arg HTTPD_VERSION="X.X" --build-arg NODE_VERSION="vX.X.X"

## Versions
The follwing versions are build and available from [`neumantm/httpd-npm`](https://hub.docker.com/r/neumantm/httpd-npm/) on docker hub:

 - `latest` or `2.4.34-v8.11.3` with Apache 2.4.34 and Node v8.11.3
