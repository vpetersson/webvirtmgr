# Appliance WebVirtMgr

**Warning:** I started working on simplifying the installation, but gave up as I couldn't get the web-interface to load properly. Assuming you don't get a 500-error, this should work in theory at least. You might be better of using the [original version](https://github.com/retspen/webvirtmgr).

## 1. Introduction

WebVirtMgr is a libvirt-based Web interface for managing virtual machines. It allows you to create and configure new domains, and adjust a domain's resource allocation. A VNC viewer over a SSH tunnel presents a full graphical console to the guest domain. KVM is currently the only hypervisor supported.

### Technology:

The application logic is written in Python & Django. The LIBVIRT Python bindings are used to interacting with the underlying hypervisor.

### License

WebVirtMgr is licensed under the Apache Licence, Version 2.0 (http://www.apache.org/licenses/LICENSE-2.0.html).

## 1. Dependencies

### Fedora, RedHat and CentOS

    $ su -c 'yum -y install git python-virtinst'

You will also need [pip](http://pypi.python.org/pypi/pip). Depending on your version, these instructions differ.

### Ubuntu and Debian

    $ sudo apt-get install git-core python-pip virtinst

## 2. Installation

    $ git clone git://github.com/vpetersson/webvirtmgr.git
    $ cd webvirtmgr
    $ sudo pip install -r requirements.txt
    $ ./manage.py syncdb

Enter the user information:

    You just installed Django's auth system, which means you don't have any superusers defined.
    Would you like to create one now? (yes/no): yes (Put: yes)
    Username (Leave blank to use 'admin'): admin (Put: your username or login)
    E-mail address: username@domain.local (Put: your email)
    Password: xxxxxx (Put: your password)
    Password (again): xxxxxx (Put: confirm password)
    Superuser created successfully.

Run app for test:

    $ python manage.py run_gunicorn 0.0.0.0:8000

Enter in your browser:

    http://x.x.x.x:8000 (x.x.x.x - your IP address server)

To run the application in production, it is recommended to use [Supervisor](http://supervisord.org/). For instructions on how to set up Gunicorn in conjunction with Supervisor, please take a look at [this](http://www.robgolding.com/blog/2011/11/12/django-in-production-part-1---the-stack/) blog-post.

## 5. Update

    $ cd /path/to/webvirtmgr
    $ git pull
