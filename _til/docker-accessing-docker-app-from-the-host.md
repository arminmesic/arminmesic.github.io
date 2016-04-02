---
layout: post
title:  "Accessing docker app from the host"
date:   2015-02-17
categories:
    - til
    - docker
---

If you want to access a running application inside a docker container you need to expose the ports to the host system,
this can be achieved through flags.

* The `-P` flag maps all the internal ports (which are defined inside the Dockerfile with EXPOSE) to the host machine, it assigns a port automatically  e.g. `docker run -P --name my-docker-container mysql` 
* The `-p` flag maps a specified port to a specified port on the host machine, `<host_port>:<container_port>` e.g. `docker run -name my-app -p 3306:3306 -p 80:3002 myCustomAppImage` 
