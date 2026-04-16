
---
layout: post
title: "Homelab - Linux permission"
date: 2026-04-16
category: homelab
description: "Homelab - Linux permission"
---

# Linux permissions

|Binary|Octal|String representation|Meaning|
|---|---|---|---|
|000|0 (0+0+0)|- - -|no permission|
|001|1 (0+0+1)|- - x|execute|
|010|2 (0+2+0)|- w -|write|
|011|3 (0+2+1)|- w r|write + execute|
|100|4 (4+0+0)|r - -|read|
|101|5 (4+0+1)|r - x|read + execute|
|110|6 (4+2+0)|r w -|read + write|
|111|7 (4+2+1)|r w x|read + write + execute|

# Permission structure (divided in 3 groups)
|r w r|r w|r - x|
|---|---|---|
|owner|group|other|

|Permission| Binary|
|---|---|
|r w x| 4 + 3 + 1 = 7|
|r - -| 4 + 2 + 0 = 6|
|r - x| 4 + 0 + 1 = 5|
|Permission|765|

r - read  | w - write / edit | x - execute |  <br>
4 - read  | 2 - write / edit | 1 - execute |  <br>



