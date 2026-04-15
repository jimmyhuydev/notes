---
layout: post
title: "Homelab - notes application selfhost"
date: 2026-04-14
category: homelab
description: "Homelab - notes application selfhost"
---

Hosting selfhost notes in my homelab
I am using this memos application locally. --> [memos](https://github.com/usememos/memos)
The software is free to use in the homelab.

# 1. Install docker on ubuntu
```
# Quick install script (Linux)
curl -fsSL https://get.docker.com | sh

# Add yourself to docker group (avoids sudo)
sudo usermod -aG docker $USER

# Log out and back in for group change to take effect
```

# 2. Running docker to pull memos images locally
```
sudo docker run -d -p 8080:5230 neosmemo/memos:stable
```

# 3. Add crontab to run after reboot
```
sudo crontab -e

# add this command to the file crontab
@reboot sudo docker run -d -p 8080:5230 neosmemo/memos:stable
# save the file and reboot
```
After reboot, check if the docker is running that images
```
sudo docker ps
```
