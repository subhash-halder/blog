---
title: "Host Your Site Without Static IP via Server"
date: 2022-04-18T10:15:53+05:30
author: ["Subhash Halder"]
categories: ["tutorial", "ssh"]
tags: ["ssh reverse tunneling", "http tunneling", "socket tunneling"]
description: This article show how you can expose some service running in your local machine to outside world without static IP via any public server. 
draft: false
cover:
    image: "/images/ssh-reverse-tunneling.jpg"
    alt: "SSH Reverse tunneling"
    caption: "SSH Reverse tunneling"
    relative: false 
    hidden: false 
---

## Why you want to do that?
This would be the first question if I need a server for this why would I need to expose any service from local in first place?
1. One of the reason would be to reduce server cost, like say you want to do some graphic intensive task which you can do in your local.
2. You can share your local work with other without publishing your work and without using services like ngrok

## Prerequisite
Basic understanding of SSH is required, also I have done it with a linux machine will be same for mac I don't know how this works with windows machine.

## How to Do it?
Suppose you have a server running on port 8080 and want to expose it to the outside world but you don't have a public IP.
So to make it public you need to have a server with public IP running in cloud (or any where) and SSH running in both the mechine.
Let say the IP address of the public server is pp.pp.pp.pp
then in the private server run the command ```ssh -NT -o ServerAliveInterval=5 -o ExitOnForwardFailure=yes  -R 80:127.0.0.1:8080 ubuntu@pp.pp.pp.pp```

or to run it through systemd use this systemd file inside /etc/systemd/system/api-tunnel.service

### /etc/systemd/system/api-tunnel.service
```
[Unit]
Description=api server tunnel
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
Restart=always
RestartSec=1
User=ubuntu
ExecStart=/usr/bin/env ssh -NT -o ServerAliveInterval=5 -o ExitOnForwardFailure=yes  -R 80:127.0.0.1:8080 ubuntu@pp.pp.pp.pp

[Install]
WantedBy=multi-user.target
```

after succesfully running the command if you go the url pp.pp.pp.pp from any browser you will see the website running in port 8080 in your private machine

also need to update the sshd config file for the server machine to reduce the latency if the tunnel disconnect
### /etc/ssh/sshd_config
```
ClientAliveInterval 5
ClientAliveCountMax 3
```