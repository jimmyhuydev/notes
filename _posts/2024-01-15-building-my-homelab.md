---
layout: post
title: "Building My Homelab: A Self-Training Ground"
date: 2024-01-15
category: Infrastructure
description: "A walkthrough of my personal homelab — hardware, networking, and the VMs I use to learn every day."
---

Every engineer reaches a point where theory isn't enough — you need a real environment to break things, fix them, and truly learn. That's exactly why I built my homelab. It's a dedicated, always-on sandbox where I can practice Cisco networking, Linux administration, Python scripting, and ethical hacking — all from home.

Here's a detailed walkthrough of what I built, how it's structured, and what I use it for.

## The Hardware

The heart of my lab is a compact **Dell Mini PC**. Small, quiet, and power-efficient — perfect for a machine that runs 24/7. Don't let the form factor fool you: it handles multiple VMs without breaking a sweat.

| Component  | Spec                                |
|------------|-------------------------------------|
| Machine    | Dell Mini PC                        |
| CPU        | Intel Core i5-7500T @ 2.70GHz      |
| RAM        | 32 GB                               |
| Storage    | 1 TB HDD                            |
| Host IP    | 192.168.8.1                         |
| Hypervisor | Proxmox VE                          |

The 32 GB of RAM is the most important upgrade here. Running five VMs simultaneously — Cisco Modeling Lab, two Ubuntu instances, Kali Linux, and Windows 10 — demands memory above all else.

## Network Isolation with the GL-SFT1200

One thing I was deliberate about from day one: **keeping the lab network completely isolated from my home Wi-Fi**. For this I use a GL-iNet GL-SFT1200 travel router — a small OpenWrt-based router that creates a dedicated lab subnet.

```
Home Wi-Fi ──── GL-SFT1200 ──── Lab Network (192.168.8.x)
                (separator)          │
                                     ├── 192.168.8.1  Proxmox host
                                     └── 192.168.8.3  CML (Cisco)
```

This means any noisy experiments — packet floods, VLAN configs, nmap scans — stay contained within the lab subnet and never touch home devices. Simple but critical.

## Proxmox: The Virtualization Layer

On bare metal I run **Proxmox VE**, an open-source hypervisor based on KVM and LXC. Proxmox gives me a clean web interface to spin up, snapshot, clone, and destroy VMs at will — for free.

> Proxmox's snapshot feature is a game-changer for learning. Before trying something risky, take a snapshot. If things go sideways, roll back in seconds.

## Virtual Machines

Each VM serves a specific learning purpose:

| VM              | IP            | Purpose                                      |
|-----------------|---------------|----------------------------------------------|
| CML (Cisco)     | 192.168.8.3   | Routers, switches, OSPF, BGP, VLANs         |
| Ubuntu 1        | —             | Bash scripting, Vim, Python development      |
| Ubuntu 2        | —             | Server-side experiments, SSH, client-server  |
| Kali Linux      | —             | nmap, network scanning, security tooling     |
| Windows 10      | —             | Cross-platform testing, AD practice          |

### Cisco Modeling Lab (CML)

CML lets me build real Cisco network topologies and configure actual Cisco IOS — not just simulators. I use it to practice routing protocols, VLAN design, and prepare for certifications.

### Ubuntu (×2)

My Ubuntu VMs are where I sharpen everyday Linux skills: navigating the terminal fluently, writing bash scripts, mastering Vim, and building Python tools. Having two instances lets me practice client-server interactions like SSH and SCP.

### Kali Linux

Kali is the industry-standard penetration testing OS. My isolated lab gives me a legal, safe environment to explore it. I focus on `nmap` for network discovery and port scanning — learning to see what attackers see, so I can think defensively.

### Windows 10

Real-world IT environments are hybrid. A Windows VM lets me practice cross-platform administration and verify how tools behave across operating systems.

## Why Every IT Learner Needs a Lab

Documentation and tutorials only take you so far. The moment you misconfigure a router and lose connectivity, or watch a bash script actually automate a task — that's when knowledge turns into skill.

The total cost? A secondhand Dell Mini PC and a travel router. The return? An always-available, personal training ground where I control everything.

**Start small, keep it running, and break things on purpose.**
