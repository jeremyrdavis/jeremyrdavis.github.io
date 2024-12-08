---
title: 'Building amd64 with Docker on a Mac M1'
subtitle: 'Because You Aren't Going to Deploy on Apple Silicon'
date: 2023-11-29
excerpt: Docker defaults to M1 images
tags: quarkus,docker,containers
---

I use a Mac for development so Docker defaults to M1 images.  It's easy to configure Quarkus to build for linux/amd64.  Just add the following to your application.properties:

```
quarkus.docker.buildx.platform=linux/amd64
quarkus ext add container-image-docker
quarkus build -Dquarkus.container-image.build=true
```
