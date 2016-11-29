---
layout: post
title:  "Get logs from Docker"
date:   2016-11-25
categories:
    - til
    - docker
---

To get a constant stream of logs from a docker container you need `docker logs <container-name> -f`, the `f` flags will
constantly display the new logs, without this flag it would just display the logs the container had collected till this 
moment and then close the connection.