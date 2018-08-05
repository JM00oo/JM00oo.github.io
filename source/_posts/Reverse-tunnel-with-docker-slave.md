---
title: Reverse tunnel with docker slave
tags:
  - docker
  - ssh
  - network
date: 2017-04-19 13:46:47
---


#### Configuration
> private-client - 192.168.0.10
> jenkins-ec2 - 54.xx.xx.84

#### On jenkins-ec2
{% codeblock line_number:false highlight:true lang:"shell" %}
$ ifconfig
> ...
> docker0   Link encap:Ethernet  HWaddr 02:42:34:49:99:84
> inet addr:172.17.0.1  Bcast:0.0.0.0  Mask:255.255.0.0
> ...
{% endcodeblock %}

<!--more-->

#### On private-client
{% codeblock line_number:false highlight:true lang:"shell" %}
$ ssh -i KEY_FILE -NfR 12345:localhost:22 ubuntu@54.xx.xx.84
{% endcodeblock %}

#### Back to jenkins-ec2
Now we can login ```private-client``` on jenkins-ec2
{% codeblock  line_number:false highlight:true lang:"shell" %}
$ ssh user@localhost -p 12345
{% endcodeblock %}

However, for docker container in jenkins-ec can't login ```private-client```.
To enble that just need modify the configuration on ```jenkins-ec2```:
{% codeblock /etc/ssh/sshd_config line_number:false highlight:true lang:"configuration" %}
GatewayPorts yes
{% endcodeblock %}
And run:
{% codeblock on jenkins-ec2 line_number:false highlight:true lang:shell %}
# /etc/init.d/ssh restart
{% endcodeblock %}

#### In docker container on jenkins-ec2
{% codeblock in container line_number:false highlight:true lang:shell %}
$ ssh -i user@172.17.0.1 -p 12345
{% endcodeblock %}

#### Reference
[SSH reverse tunnel]
[SSH reverse tunnel]: https://toic.org/blog/2009/reverse-ssh-port-forwarding/
