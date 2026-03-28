---
layout: post
title: "MoinMoin Wiki Installation with Lighttpd on Raspberry Pi OS"
date: 2020-10-31
category: Linux
description: "Step-by-step guide to setting up MoinMoin wiki on Raspberry Pi OS (Raspbian) using lighttpd and FastCGI."
tags: [python, moin, wiki, lighttpd, raspbian, raspberry-pi]
---

Personal notes for setting up MoinMoin wiki on Raspberry Pi OS for home use. I'm running Raspbian on Hyper-V, but these steps work equally on a physical Raspberry Pi.

---

## Step 1 — Install Raspberry Pi OS on Hyper-V

Download the Raspberry Pi Desktop image:
👉 [https://www.raspberrypi.org/downloads/raspberry-pi-desktop/](https://www.raspberrypi.org/downloads/raspberry-pi-desktop/)

**Optional extras to install on this host:**

- Install **TightVNC** for remote desktop access
- Set up TightVNC with a password:

```bash
/usr/bin/tightvncserver
```

---

## Step 2 — Download and Extract MoinMoin

Download the MoinMoin source:

```bash
wget http://static.moinmo.in/files/moin-1.9.10.tar.gz
```

Extract the archive:

```bash
tar xvzf moin-1.9.10.tar.gz
```

Rename the extracted folder:

```bash
sudo mv moin-1.9.10 moin
```

---

## Step 3 — Create the Required Directories

```bash
# Engine folder — where MoinMoin is installed
sudo mkdir /usr/local/moinmoin_engine

# Instance folder — the website root served by lighttpd
sudo mkdir /usr/local/moinmoin_instance1
```

---

## Step 4 — Install MoinMoin

From inside the `moin` source folder (`/home/pi/moin`), run:

```bash
sudo python setup.py install --prefix=/usr/local/moinmoin_engine
```

---

## Step 5 — Copy Required Files to the Instance Folder

```bash
sudo cp -r /usr/local/moinmoin_engine/share/moin/data /usr/local/moinmoin_instance1
sudo cp -r /usr/local/moinmoin_engine/share/moin/underlay /usr/local/moinmoin_instance1
sudo cp /usr/local/moinmoin_engine/share/moin/config/wikiconfig.py /usr/local/moinmoin_instance1
sudo cp /usr/local/moinmoin_engine/share/moin/server/moin.fcgi /usr/local/moinmoin_instance1
```

---

## Step 6 — Set Folder Permissions

Give the web server user ownership of the instance folder:

```bash
sudo chown -R www-data:www-data /usr/local/moinmoin_instance1
```

---

## Step 7 — Configure `moin.fcgi`

Edit `/usr/local/moinmoin_instance1/moin.fcgi` and update the following lines:

```python
# Point to the MoinMoin package location
sys.path.insert(0, '/usr/local/moinmoin_engine/lib/python2.7/site-packages')

# Point to the wiki config directory
sys.path.insert(0, '/usr/local/moinmoin_instance1')

# Force FastCGI mode (not slow CGI)
os.environ['FCGI_FORCE_CGI'] = 'N'

# Fix the script name for URL rewriting
fix_script_name = ''
```

---

## Step 8 — Configure Lighttpd

Edit `/etc/lighttpd/lighttpd.conf`:

**Add modules** under `server.modules`:

```
"mod_accesslog",
"mod_fastcgi",
```

**Bind to your server IP** (add after `server.port`):

```
server.bind = "xx.xx.xx.xx"   # replace with your server IP
```

**Remove `.fcgi`** from the static file exclusions:

```
static-file.exclude-extensions = ( ".php", ".pl" )
```

**Add the FastCGI virtual host block** at the end of the file:

```
$HTTP["host"] =~ "/" {

    fastcgi.server += ( "/" =>
      ((
        "socket"            => "/tmp/moin.socket",
        "min-procs"         => 1,
        "max-procs"         => 2,
        "check-local"       => "disable",
        "bin-path"          => "/usr/local/moinmoin_instance1/moin.fcgi",
        "fix-root-scriptname" => "enable"
      ))
    )

}
```

---

## Step 9 — Allow User Registration in `wikiconfig.py`

In `/usr/local/moinmoin_instance1/wikiconfig.py`, enable account creation:

```python
actions_superuser = multiconfig.DefaultConfig.actions_superuser[:]
actions_superuser.remove('newaccount')
```

After this change, users can register via the MoinMoin login page.

---

## Step 10 — Set Admin User Permissions

```python
acl_rights_before = u"Your-User:read,write,delete,revert,admin"
```

Replace `Your-User` with your actual wiki username.

---

## Step 11 — Configure Email (SMTP)

```python
# SMTP server
mail_smarthost = "smtp.office365.com:587"

# Return address
mail_from = u"Jimmy Wiki Support <your_email@domain.com>"

# SMTP login credentials
mail_login = "your_email@domain.com Yourpassword"
```

---

## Step 12 — Restart Lighttpd

```bash
sudo service lighttpd restart
```

You'll be prompted to authenticate:

```
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to restart 'lighttpd.service'.
 1.  ,,, (pi)
 2.  root
Choose identity to authenticate as (1-2):
```

Select `1` and enter the `pi` user password. You should see:

```
==== AUTHENTICATION COMPLETE ===
```

---

## Done!

Open your browser and navigate to your server IP. Create the username that matches `Your-User` — this account will have full admin permissions to create and manage wiki pages.

**Optional — restrict wiki to known users only:**

Add this to `wikiconfig.py` to prevent anonymous access:

```python
acl_rights_default = u"Trusted:read,write,delete,revert Known:read"
```

This means only logged-in (Known) users can read pages.

Enjoy your wiki 🎉
