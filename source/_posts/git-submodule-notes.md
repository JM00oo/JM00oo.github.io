---
title: Git submodule notes
date: 2017-04-16 17:36:25
tags:
  - git
  - submodule
---


## Update submodule
First time need to init the submodule.
{% codeblock line_number:false highlight:true lang:"bash" %}
git submodule update --recursive --remote --init PATH
{% endcodeblock %}
otherwise
{% codeblock line_number:false highlight:true lang:"bash" %}
git submodule update --recursive --remote
{% endcodeblock %}


<!--more-->

> In this post, I noted for setup/update git submodule. In some scenarios, we developed in a project, which depends on some other library. If we want to separately version controlling both of them, ```git submodule``` is a good tool for that.


For example, I use Hexo to manage my blog, and in the repository there is a themes module to setup the blog theme.

## Add submodule
{% codeblock line_number:false highlight:true lang:"bash" %}
cd BLOG_DIR
git submodule add GIT_URL themes/THEME_NAME
{% endcodeblock %}

Suppose someone else update and push the submodule in the remote repository, we may need to update the submodule.

## Update submodule
First time need to init the submodule.
{% codeblock line_number:false highlight:true lang:"bash" %}
git submodule update --recursive --remote --init PATH
{% endcodeblock %}
otherwise
{% codeblock line_number:false highlight:true lang:"bash" %}
git submodule update --recursive --remote
{% endcodeblock %}

Sometimes, we may encounter some problem of adding submodule, i.e. ```'projectfolder' already exists in the index```. Here is a way to fix it:

## Fix issue of adding submodule
{% codeblock line_number:false highlight:true lang:"bash" %}
git rm --cached projectfolder
{% endcodeblock %}

References:
[Git submodule](http://bit.ly/2pF1Jw6)
[Update submodule](http://bit.ly/2ojiMm4)
[Fix submodule issue](http://bit.ly/2ppm496)
