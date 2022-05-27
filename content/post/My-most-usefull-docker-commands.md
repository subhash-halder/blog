---
title: "My Most Usefull Docker Commands"
date: 2022-04-30T01:20:11+05:30
author: ["Subhash Halder"]
categories: ["tutorial", "docker"]
tags: ["docker", "docker command", "basic docker command", "docker tutorial"]
description: In this article I will try to note down all the useful docker command I used in my daily life.
draft: true
cover:
    image: "/images/horizontal-logo-monochromatic-white.webp"
    alt: "Docker logo"
    caption: false
    relative: false 
    hidden: false 
---

## Installing Docker
For Installing docker please follow the instruction according to your OS [install link](https://docs.docker.com/engine/install/).
To check if docker is installed correctly try to run the command from a terminal.

```
docker --version
```

> NOTE: In linux if it requires sudo permission please use this command to run any docker command without sudo
> 
> 1. Create the docker group.
> ```
> sudo groupadd docker
> ```
> 2. Add your user to the docker group.
> ```
> sudo usermod -aG docker $USER
>  ```
> Logout and login again to take effect, or follow the [StackExchange post](https://superuser.com/questions/272061/reload-a-linux-users-group-assignments-without-logging-out) if it works.

 ### Fun part begins after the installation is complete
