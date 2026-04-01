---
layout: post
title: "Palo Alto - Zero Trust and NAT"
date: 2026-03-29
category: Tools
description: "Zero Trust and NAT"
tags: [software, tools, productivity, palo alto, homelab]
---

# Zero Trust and NAT

#### Part A:

Perform the following actions on the firewall:

![](assets/Labs/Lab8/media/image7.png){width="4.953125546806649in"
height="1.579601924759405in"}

Before apply the lab3 configuration, ping google is successfully.

![](assets/Labs/Lab8/media/image1.png)

After the lab3 configuration is applied, ping is not successfully.

- Ensure that you use TAGS (color code)

> ![](assets/Labs/Lab8/media/image14.png)
>
> Tag color code is setup.

- Change the admin password

> ![](assets/Labs/Lab8/media/image16.png)
>
> Changed admin password to P@ssw0rd

- Create a user that has access to all of the logs (including packet
  captures)

> ![](assets/Labs/Lab8/media/image12.png)
>
> Created user log-admin policy
>
> ![](assets/Labs/Lab8/media/image8.png)
>
> Created logsuser using log-admin role.

- Replace the security certificate on the firewall

> ![](assets/Labs/Lab8/media/image6.png) Generate certificate jimmylab03

#### Part B: Nat and Security Policies

- Create and associate Zones with interfaces

> ![](assets/Labs/Lab8/media/image9.png)
>
> Zones with interfaces

- Create rules/policies to allow the below ports/services to be accessed
  from the internet

  - Ensure that you utilize tags (color code)

  - DMZ- Ports: 80, 21, 22

  - Windows- Ports: 25, 3389

![](assets/Labs/Lab8/media/image10.png)

Setup the color tags

![](assets/Labs/Lab8/media/image20.png)

NAT rules for outside to dmz ftp / http / ssh

![](assets/Labs/Lab8/media/image13.png)

Policy for outside to dmz ftp / http / ssh

![](assets/Labs/Lab8/media/image19.png)

NAT port 25 and 3389 for windows

![](assets/Labs/Lab8/media/image17.png)

Policy for port 25 and 3389 for windows

![](assets/Labs/Lab8/media/image18.png)

Port 80 can be access with curl command

- Create a rule/policy to allow the Windows system to FTP to the DMZ
  system

> ![](media/image15.png)
>
> NAT Windows inside to dmz ftp
>
> ![](assets/Labs/Lab8/media/image11.png)
>
> Policy windows inside to dmz ftp

#### Part C: Packet Capture and Analysis (using nmap)

- Log in as a user with log rights that you created earlier

- Setup packet capture on the firewall. Capture drop, firewall, and
  received packets

- Install NMAP on the external router

  - yum install nmap (you can use curl if we do not get nmap installed
    in time)

  - Run the below nmap scans against the firewall to ensure that the
    correct ports/services are open

    - nmap -sS x.x.x.x

    - nmap -sS -p80, 21, 22 etc x.x.x.x.

![](assets/Labs/Lab8/media/image2.png)

Nmap scan to show the port open at firewall

![](assets/Labs/Lab8/media/image3.png)

Ftp from inside to DMZ

- FTP from the external and from the Windows system onto the DMZ FTP
  server.

  - Are you able to view the different logs generated

I don't see the logs generated when I connect the FTP but I can see the
Hit Count in NAT rules and Policy rules.

- Analyze the firewall logs within Palo Alto.

  - Can you see the scanning activity?

I don't see scanning activity in Palo Alto

- Are you able to see your ports/services open via the logs generated?

> Yes, I can see the port services open via logs
>
> ![](assets/Labs/Lab8/media/image21.png)

- Use the ACC network activity to analyze your firewall logs. Narrow
  down your view to your outside ports/services

> I can see the services in ACC as following
>
> ![](assets/Labs/Lab8/media/image5.png)

- Utilize Wireshark to view the logs that Palo Alto created.

  - Did the Palo Alto pcap logs capture the above activity?

> ![](assets/Labs/Lab8/media/image4.png)
>
> Yes the pcap logs shows the nmap scan
