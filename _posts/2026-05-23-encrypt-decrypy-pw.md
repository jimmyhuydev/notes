---
layout: post
title: "encrypt password and decrypt password - python program"
date: 2026-05-23
category: python project homelab
description: "encrypt password and decrypt password - python program"
---

# Project to encrypt password and decrypt password

## encrypt password

```
#create an program to encrypt the password

import base64

def encrypt_pass(password):
    encode_bytes = base64.b64encode(password.encode())
    print(encode_bytes)


user_pass = input("Enter your password: ")
encrypt_pass(user_pass)


```


## Decrypt password

```
#create an program to decrypt the password
import base64

def decode_password(password):
    decode_bytes = base64.b64decode(password)
    decode_data = decode_bytes.decode()
    print(decode_data)



encode_string = input("Enter the base64 string: ")
decode_password(encode_string)


```
