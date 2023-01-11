---
---
# Nginx

# Plan
- [ ] Read Nginx Cookbook by O'really
- [x] Install Nginx on Ubuntu
  - [x] Start Nginx as daemon
  - [x] Containerized installation
- [x] Basic commands
  - [x] -h, -v, -t, -s
- [x] Serve static webpage
  - [x] Reload signal

# Install Nginx on Ubuntu

Follow steps mentioned at official site here, https://nginx.org/en/linux_packages.html#Ubuntu

## Start Nginx as Daemon
Instead of manually starting process, we can set to auto_start mode by enabling & syarting it with systemctl.

```console
$ sudo systemctl enable nginx  
$ sudo systemctl start nginx
```

## Containerized installation
```console
docker pull nginx
docker run --name some-nginx -d -p 8087:80 nginx

# Verify
curl localhost:8087
```

Or On browser hit URL localhost:8087

# Basic commands
**-h**</p>
Help command.</p>

**-v / -V**</p>
Version</p>
**-t / -T**</p>
Tests confidguration for validity</p>
**-s**</p>
signal command takes options like , </p>
start, stop, quit, reload etc.</p>


# Serve static webpage
webpage configuration are store at `/etc/nginx/conf.d/` directory </p>
Logs path     : `/var/log/nginx/` </p>
root location : `/usr/share/nginx/html/`

Store webpages to root location & create config for this inside config dir.
```console
#Reload nginx to capture new resources
# hot load
nginx -s reload

# Verify
curl example.com:8081

```

Verify static page is being served.</p>
On browser hit URL <HOSTNAME>:<PORT>

