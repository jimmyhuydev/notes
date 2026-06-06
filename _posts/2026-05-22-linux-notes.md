---
layout: post
title: "Linux commands"
date: 2026-05-22
category: linux command
description: "Linux commands"
---

# Alpine linux 
```
rc-update
rc-service networkmanager enable
rc-service networkmanager start
udhcpc -i wlan0
ip link
rc-service iwd start
rc-update add iwd default

su

apk add networkmanager network-manager-applet
rc-update add networkmanager default
rc-service networkmanager start

```

# Linux commands
```
vi --> open the vi editor
git branch -D <branch name> delete the branch
git add .
git commit
git check out main 
git push -u origin main
ls 
ls -la
cp 
mv
touch

git remote set-url origin git@github.com:jimmyhuydev/linux-notes.git
git push -u origin main
nano
```

# Daily workflow
```
git switch -c feature-name      # Create branch
```

# ... make changes ...
```
git add .                       # Stage changes
git commit -m "Description"     # Commit
git push                        # Push to GitHub
```

# Create PR on GitHub, merge, then:
```
git switch master
git pull

When thing break
git reset --hard origin/master   #Nuclear options
```

# Vmware on linux mint
```
URL: https://ubuntuhandbook.org/index.php/2024/04/install-vmware-player-ubuntu/
```
