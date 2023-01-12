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
- [x] High-Performance Loadbalancing
  - [ ] Load balancing methods
  - [ ] network protocol based LB
- [ ] Health checks
  - [ ] Active HC
  - [ ] Passive HC
  - [ ] Slow start issue


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

# High-Performance Loadbalancing
Why LB is important?
Todays world softwares demand high availability & high performance.</p>
To acheive this, creating multiple copies / instances of your applications is the way. As and when load on the instances increases adding another copy to cluster is the solution which is also called `Horizontal Scaling`.</p>
Now managing request load between these instances becomes important and solution is called `Load balancer`.</p>
There are two types of Load balancing technique,</p>
1. Application Layer LB: Used when LB decisions are to be made based on content of request.
2. Network Layer / Transport Layer LB: Used when LB decisions are made based on network information present in packets at Network layer.

Nginx serves for Network Layer LB?

How LB Helps?
- Request routing</p>
- Server health check</p>
- Sticky sessions for stateful applications</p>
