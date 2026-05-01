---
layout: post
title: "Docker on chromebook"
date: 2026-05-01
category: homelab
description: "Docker on chromebook"
---

```
sudo apt-get install -y lsb-release software-properties-common
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
```
