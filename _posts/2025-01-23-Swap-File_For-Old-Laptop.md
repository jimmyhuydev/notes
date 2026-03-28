---
layout: post
title: "Swap File for Old Laptop"
date: 2025-01-23
category: Linux
description: "How to create and resize a swap file on Linux — useful when your laptop only has 4 GB of RAM."
tags: [linux, swapfile]
---

Swap space is a reserved area on disk used when physical RAM is full. When a Linux system runs out of RAM, inactive pages are moved from RAM to the swap space — keeping the system running instead of crashing.

This is important for my old laptop, which only has **4 GB of RAM** and starts to crawl under load. Adding a larger swap file gives it some breathing room.

---

## Quick Steps

1. Turn off swap processes
2. Resize the swap file
3. Make the file usable as swap
4. Activate the swap file
5. Verify the swap size

---

## Step-by-Step

### Step 1 — Turn off swap

```bash
sudo swapoff -a
```

### Step 2 — Create a new swap file (8 GB = double the RAM)

```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=8192
```

> `bs=1M count=8192` creates an 8 GiB file. Adjust `count` for a different size (e.g. `count=4096` for 4 GiB).

### Step 3 — Set correct permissions

```bash
sudo chmod 0600 /swapfile
```

### Step 4 — Format it as swap

```bash
sudo mkswap /swapfile
```

### Step 5 — Activate it

```bash
sudo swapon /swapfile
```

### Step 6 — Verify

```bash
grep Swap /proc/meminfo
```

Or check the file size directly:

```bash
ls -lh /swapfile
```

---

## Make It Permanent (survive reboots)

Add the swap file to `/etc/fstab` so it activates automatically on boot:

```bash
# /etc/fstab — add this line at the end
/swapfile swap swap sw 0 0
```

---

## Alternative: Swap on a Separate Partition or Path

If you want to store the swap file on a different drive (e.g. a fast HDD), change the path accordingly:

```bash
# Create the file on a specific drive
sudo dd if=/dev/zero of=/media/fasthdd/swapfile.img bs=1024 count=1M

# Format it
sudo mkswap /media/fasthdd/swapfile.img

# Activate it
sudo swapon /media/fasthdd/swapfile.img
```

And in `/etc/fstab`:

```
/media/fasthdd/swapfile.img swap swap sw 0 0
```

---

## Confirm Everything is Working

```bash
cat /proc/swaps
```

Expected output:

```
Filename                          Type    Size      Used  Priority
/swapfile                         file    8388604   2724  -1
```

```bash
grep 'Swap' /proc/meminfo
```

Expected output:

```
SwapCached:     4772 kB
SwapTotal:   8388604 kB
SwapFree:    8355812 kB
```

If `SwapTotal` shows your new size, you're done. ✓
