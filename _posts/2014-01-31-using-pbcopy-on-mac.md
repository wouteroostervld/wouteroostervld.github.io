---
layout: post
title:  "Use pbcopy to get your pubkey on your clipboard"
date:   2014-01-31 16:30
categories: shell mac
---
On your mac add this to your .bash_profile:
{% highlight sh %}
alias gk='pbcopy <~/.ssh/id_rsa.pub'
{% endhighlight %}

Start a new Terminal. Now 'gk' copies your key to the clipboard.
