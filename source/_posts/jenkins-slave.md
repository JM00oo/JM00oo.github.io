---
title:  "Jenkins slave setup notes"
date:   2017-04-12
categories: Tech
tags:
      - docker
      - CI/CD
      - Jenkins
comments: true
photos: http://bit.ly/2ofKxNp
---
In this article, I introduced how to setup a docker-host based Jenkins slave step by step from installing docker. It includes some trick of how to run docker with parameters.

<!--more-->

## Install Docker

{% codeblock line_number:false highlight:true lang:"bash" %}
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo apt-key fingerprint 0EBFCD88

$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

$ sudo apt-get update

$ sudo apt-get install docker-ce
{% endcodeblock %}
Ref: [Docker install guide][Install-docker]

## Modify docker config
Add config
{% codeblock /etc/default/docker line_number:true highlight:true lang:"bash" %}
DOCKER_OPTS="-H tcp://172.31.16.61:2375 --live-restore"
{% endcodeblock %}

Modify
{% codeblock /lib/systemd/system/docker.service line_number:true highlight:true lang:"bash" %}
EnvironmentFile=-/etc/default/docker
ExecStart=/usr/bin/dockerd -H fd:// $DOCKER_OPTS
{% endcodeblock %}

Run
{% codeblock line_number:false highlight:true lang:"bash" %}
$ service docker restart
{% endcodeblock %}

## Install Java
{% codeblock line_number:false highlight:true lang:"bash" %}
sudo apt-get install default-jre
sudo apt-get install default-jdk
{% endcodeblock %}

Ref: [Install Java][Install-Java]

[Install-Java]:  https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get
[Install-docker]: https://docs.docker.com/engine/installation/linux/ubuntu/
