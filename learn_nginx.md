---
---
# Nginx

# Plan
- [ ] Read Nginx Cookbook by O'really
- [x] Install Nginx on Ubuntu
  - [x] Start Nginx as daemon
  - [x] Containerized installation
- [ ] Basic commands
- [ ] -h, -v, -t, -s
- [ ] Serve static webpage
  - [ ] Reload signal

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
