---
layout: post
title: "Puppy Linux on MacBook Air 2014"
date: 2024-05-05
category: Linux
description: "How I installed Puppy Linux (Ubuntu base) on a 2014 MacBook Air to bring it back to life."
tags: [linux, puppy-linux, macbook, frugal-install, uefi]
---

Puppy Linux (Ubuntu base) is super lightweight and made my old MacBook Air usable again. Here are the steps I followed to get it running with a frugal install.

---

## Step 1 — Partition the Drive with GParted

Use **GParted** to set up the internal drive with 2 partitions:

| Partition | Size | Format | Flags |
|-----------|------|--------|-------|
| 1st | ~300 MB | FAT32 | `boot`, `esp` |
| 2nd | Remaining space | ext3 or ext4 | — |

- The **FAT32 partition** is where the bootloader files live — this is a UEFI requirement. Some computers look specifically for a FAT32 partition to find bootloader files.
- The **ext3/ext4 partition** is where the frugal install(s) go.

---

## Step 2 — Run Frugalpup Installer

- Launch the **Frugalpup Installer** main program.
- On the main window, click the **Puppy** button to begin the install.
- Work through the install process, selecting the **ext-formatted partition** as the install destination.

---

## Step 3 — Create a Directory for the Install

When prompted to select a partition:

- A window will pop up offering to create a directory for the frugal install.
- Create the directory and name it after the Puppy version (e.g. `fossapup64`).
- **Important:** Press **Enter** to create the directory — do NOT press the OK button.
- Read the window info carefully, then complete the install.

---

## Step 4 — Install the Bootloader

When back at the main Frugalpup window:

1. Click the **Boot** button.
2. Select the location of the frugal install on the internal drive *(usually pre-selected — just click OK)*.
3. Select the small **300 MB FAT32 partition** as the bootloader location *(scroll the selection window if needed)*.
4. Choose a bootloader type:

| Option | Use case |
|--------|----------|
| `UEFI` | UEFI computers only |
| `mbr` | Legacy BIOS computers only |
| `both` | Boot on anything |

Choosing **UEFI** or **both** will also install the files needed to support **Secure Boot**.

### Secure Boot Note

When you first boot from the internal drive on a UEFI computer with Secure Boot enabled, a process will start to install the Puppy security key into the computer's firmware — alongside the other trusted keys already loaded.

> I had one computer that would **not** boot if Secure Boot was disabled. The fix was to enable Secure Boot and install the UEFI bootloader type, which then walked through adding the Puppy security key.

### Adding More Frugal Installs Later

To add another Puppy version to the same drive, just run Frugalpup Installer again for the new version. When you run the bootloader install step, it will automatically create boot menu entries for **all installs** it finds on the drive.

---

## Install Wi-Fi — Broadcom Driver (MacBook Air 2014)

The MacBook Air 2014 uses a Broadcom Wi-Fi chip. Install the driver with:

```bash
sudo apt-get install broadcom-sta-source broadcom-sta-dkms broadcom-sta-common
```

---

## Download Puppy Linux

Get the latest Puppy Linux builds from the official collection:

👉 [https://forum.puppylinux.com/puppy-linux-collection](https://forum.puppylinux.com/puppy-linux-collection)

---

## Software I Install on Puppy Linux

- Install **Flatpak**
- Install **Anki** via Flatpak
- Install **LocalSend**

---

## Reference

Original instructions sourced from the Puppy Linux forum — saved here for my own notes.

👉 [https://www.forum.puppylinux.com/viewtopic.php?p=79229&hilit=macbook+efi#p79229](https://www.forum.puppylinux.com/viewtopic.php?p=79229&hilit=macbook+efi#p79229)
