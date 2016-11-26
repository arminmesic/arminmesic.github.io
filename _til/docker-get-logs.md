---
layout: post
title:  "Enter Docker container and execute commands"
date:   2016-11-25
categories:
    - til
    - docker
---

If you want to enter a container and execute commands from inside you just need to type `docker exec -it <container-name> bash`

`docker exec` runs a command in the container, the `i` flag keeps the STDIN open and the `t` flag creates a tty.