---
layout: post
title:  Jekyll Server Error
author: Zhen Zhao
date:   2015-11-08 22:32:43 -05:00
categories: Server
---

Try to restart Jekyll Server after get  a conversion error
Show the following error:
{% highlight console %}
Jekyll 3.0.0 | Error:  Address already in use - bind(2)
{% endhighlight %}

### Solution:
1. `sudo lsof -i :4000` check PID of server port
2. `kill -9 + PID`
3. start Jekyll Server 