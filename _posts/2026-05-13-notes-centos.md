---
layout: post
title: "Notes for centos 2009 in lab"
date: 2026-05-13
category: homelab centos
description: "Notes for centos 2009 in lab"
---

# Notes for centos 2009 in lab

vi /etc/yum.d.repos/CentOS-Base.repo

for [base] <br>
baseurl=http://vault.centos.org/7.9.2009/os/$basearch/

for [updates] <br>
baseurl=http://vault.centos.org/7.9.2009/updates/$basearch/

for [extras] <br>
baseurl=http://vault.centos.org/7.9.2009/extras/$basearch/
