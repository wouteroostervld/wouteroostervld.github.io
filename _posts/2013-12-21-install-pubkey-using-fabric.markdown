---
layout: post
title:  "Using fabric to upload your ssh-pubkey"
date:   2013-12-21 22:42
categories: python fabric
---

[Fabric] is a tool written in and using python to automate recurring tasks on remote servers. You can use pip to install it:

{% highlight sh %}
$ sudo pip install fabric
{% endhighlight %}

Here an example of a fabfile with one command 'install_key' which installs your id_rsa.pub on a remote server. Create a fabfile.py containing the following:

{% highlight python %}
from fabric.api import *
import os
from fabric.contrib.files import append

env.shell = "/bin/sh -c"

def install_key():
    run('mkdir .ssh || :')
    run('chmod u=rwx,og=rx .ssh')
    home = os.getenv('HOME')
    with open(home + '/.ssh/id_rsa.pub') as f:
        line = f.readline() 
    append('.ssh/authorized_keys',line)
    run('chmod u=rw,og=r .ssh/authorized_keys')
{% endhighlight %}

Doing 'fab -l' should now show the install_key command.

I needed to override the env.shell-var to use /bin/sh to get it to work on freebsd.

You now can run this on an arbitrary server you have access to:

{% highlight sh %}
$ fab -u admin -H 192.168.188.200 install_key 
{% endhighlight %}

[Fabric]: http://fabfile.org/
