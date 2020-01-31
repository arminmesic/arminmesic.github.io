---
layout: post
title:  "Setting up and debugging Selenium with Docker"
date:   2020-31-01
categories:
    - Python
    - Docker
---

This tutorial covers how to setup and debug Selenium with Docker, it can be used to automate testing or to crawl through
 websites. I'll be using Python but it should work the same way for different languages too.

First we need to create a `docker-compose.yml` file, it will launch our Selenium instance, `docker-compose.yml` should
contain following lines

```yaml
version: '3'

services:
  tutorial-selenium:
    image:  "selenium/standalone-chrome-debug"
    container_name: tutorial-selenium
    volumes:
      - /dev/shm:/dev/shm
    ports:
    - 5900:5900

  tutorial-python:
    image: "python"
    container_name: tutorial-python
    tty: true
    depends_on:
      - tutorial-selenium
    volumes:
    - ./code:/code
```

Quick explanation what is happening. We're using the `selenium/standalone-chrome`, this makes debugging easier for
us because it allows us to connect with a VNC client and see what is happening. Port `5900` is being exposed because 
we're going to use it to connect with our VNC client. Download a VNC client of your choice and connect to `localhost:5000`
with the default password `secret`.

`/dev/shm` is mounted to use the hosts share memory or else instances of Chrome or Firefox would crash, you can read more
about the [Chrome issue](https://bugs.chromium.org/p/chromium/issues/detail?id=519952) and the 
[Firefox issue](https://bugzilla.mozilla.org/show_bug.cgi?id=1338771#c10).

The python container mounts the `code` folder which contains our code. `tty:true` keeps the container running to make debugging
the python code easier.

Next step we're going to write our code to connect with Selenium. First we need to add `selenium` to our `requirements.txt` 
file, so create a file `code/requirements.txt` and add `selenium`. Next create a new file `code/app.py`, it will contain
main code.

```python
from selenium import webdriver

driver = webdriver.Remote(
    desired_capabilities=webdriver.DesiredCapabilities.CHROME,
    command_executor='http://tutorial-selenium:4444/wd/hub'
)
driver.get('https://google.com')
print(f"Page title: {driver.title}")
driver.quit()
```
This code opens a page (`https://google.com`) and prints the page title.  We're connection to a remote instance of 
Chrome which is reachable with `http://tutorial-selenium-chrome:4444/wd/hub` from within the container. To see it in
action run `docker exec -it tutorial-python bash`, once you've established a connection to the container run `cd /code`.
Now you need to install the dependencies with `pip install -r requirements.txt` and finally you can execute the code 
`python app.py`. If you're using a VNC client and have created a connection with `localhost:5900` (password is `secret`)
you should see a browser opening and visiting `https://google.com` and closing again.

Now you can adjust your code to do the things you need to, when you're done and you application is running successfully
you can update your `docker-compose.yml` file and change the debug version of selenium with a normal one.

```yaml
services:
  tutorial-selenium:
    image:  "selenium/standalone-chrome"
    container_name: tutorial-selenium
    volumes:
      - /dev/shm:/dev/shm

  tutorial-python:
    image: "python"
    container_name: tutorial-python
    tty: true
    depends_on:
      - tutorial-selenium
    volumes:
    - ./code:/code
```

I've used Chrome for our example, but this can be done also for Firefox, you just need to change the images,
 `selenium/standalone-chrome-debug` becomes `selenium/standalone-firefox-debug`, `selenium/standalone-chrome` becomes
 `selenium/standalone-firefox` and finally you need to update `app.py` to use Firefox.
 
```python
from selenium import webdriver

driver = webdriver.Remote(
    desired_capabilities=webdriver.DesiredCapabilities.FIREFOX,
    command_executor='http://tutorial-selenium:4444/wd/hub'
)
driver.get('https://google.com')
print(f"Page title: {driver.title}")
driver.quit()
```

If there are any open questions you can send a mail, it's provided on the about me page.