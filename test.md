---
layout: default
title: Testing
---

# How to test the current code

**Beware**: Even though the current code works, it's still quite crude. Bear that in mind.


### 1.- Init your Pasalo instance
~~~ bash
python df-init.py
~~~
It creates the *~/.pasalo* directory along with both the GnuPG and HTTPS keys.


### 2.- Send me your key
~~~ bash
python df-get-key.py | mail -s "Please, add my key (`whoami`)" alvaro@pasalo.org
~~~
.. or send it using you mail application of choice. It doesn't matter.


### 3.- Import my key
~~~ bash
curl -k -o /tmp/alo.key https://alobbs.org/key
python df-links.py add --name=alo --url=https://alobbs.org/ --cert=/tmp/alo.key
~~~
Now we're connected.


### 4.- Subscribe a few channels
~~~ bash
python main.py channels --name=alo
python df-links.py subscribe --name=alo --channel=alo.movies.2013
~~~
Add as many channels as you want.


### 5.- It's ready to run now
~~~ bash
python main.py run
~~~
