---
layout: post
title: Django runserver over HTTPS
categories: Django
---

Quick guide to using Django's dev server over HTTPS.

----

**1.** Install Django extensions:

>     $ pip install django_extensions

Edit `settings.py`, add `django_extensions` to `INSTALLED_APPS`.

----

**2.** Create a self-signed certificate:

It's just for your local machine, so we'll set a 10-year expiry date.

>     $ sudo apt-get install openssl
>     $ openssl genrsa -out dev.key 1024
>     $ openssl req -new -key dev.key -out dev.csr -subj '/CN=localhost/O=mycompany/C=UK/'
>     $ openssl x509 -req -days 3650 -in dev.csr -signkey dev.key -out dev.crt

----

**3.** Start the server:

>     $ pt/manage.py runserver_plus --cert=dev.crt

Try it out - visit `https://localhost:8000` in your browser.

You'll *(hopefully)* see a security notice. Click through to ignore it, or Google [self-signed certificate installation](https://www.google.co.uk/search?q=install+self-signed+certificate). This varies per device, so you'll need to do a bit of research!
