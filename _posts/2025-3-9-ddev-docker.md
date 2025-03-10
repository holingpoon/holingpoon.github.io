---
layout: post
title: Docker blocked DDEV install
---

macOS >= 15.x

Docker Desktop >= v4.38

Original error when running `ddev start`

```
Failed to start d11-site: failed to start ddev-router: composeCmd failed to run 
'COMPOSE_PROJECT_NAME=ddev-d11-site docker-compose -f /Users/{user}/.ddev/.router-compose-full.yaml 
-p ddev-router up --build -d', action='[-p ddev-router up --build -d]', err='exit status 1', stdout='', stderr=' Container ddev-router  Creating
 Container ddev-router  Created
 Container ddev-router  Starting
Error response from daemon: Ports are not available: exposing port TCP 127.0.0.1:443 -> 127.0.0.1:0: 
failed to connect to /var/run/com.docker.vmnetd.sock: is vmnetd running?: dial unix /var/run/com.docker.vmnetd.sock: connect: no such file or directory'
```

In Docker Desktop, go to Settings > Advanced

Check `Allow privileged port mapping (requires password)`

Restart Docker

Then proceed with `ddev start` on the [Drupal Installation guide](https://ddev.readthedocs.io/en/stable/users/quickstart/#drupal)
