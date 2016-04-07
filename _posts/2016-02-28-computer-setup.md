---
layout: post
title: New system setup
---

Far too often it seems like I have to set up a new Ubuntu installation. To avoid floundering around, maybe it would be a good idea to document some of this?

## Sublime Text 3

{% highlight bash %}
add-apt-repository ppa:webupd8team/sublime-text-3
apt-get update
apt-get install -y sublime-text-installer
{% endhighlight %}

[source](http://www.webupd8.org/2013/07/sublime-text-3-ubuntu-ppa-now-available.html)

## nodejs (nvm)

{% highlight bash %}
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
{% endhighlight %}

[source](https://github.com/creationix/nvm)

## docker

{% highlight bash %}
apt-get update
apt-get install apt-transport-https ca-certificates
apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
bash -c "echo 'deb https://apt.dockerproject.org/repo ubuntu-wily main' > /etc/apt/sources.list.d/docker.list"
apt-get update
apt-get install -y docker-engine
service docker start
{% endhighlight %}

Test it out:

{% highlight bash %}
docker run hello-world
{% endhighlight %}

[source](https://docs.docker.com/engine/installation/linux/ubuntulinux/)
