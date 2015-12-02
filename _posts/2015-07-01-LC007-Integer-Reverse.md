---
layout: post
title:  Integer Reverse
author: Zhen Zhao
date:   2015-11-05 23:34:43 -05:00
categories: Integer
---
Reverse digits of an integer.

Example1: x = 123, return 321

Example2: x = -123, return -321


### Clarify:

1. It may stack over flow if the reversed integer is greater than the INTEGER_MAX_VALUE or smaller than INTEGER_MIN_VALUE

### Solution:
{% highlight java %}
public class Solution {
    public int reverse(int x) {
        int res = 0;
		while(x != 0) {
			int tail = x%10;
			int temp = res*10 + tail;
			if((temp - tail)/10 != res)
				return 0;
			res = temp;
			x /= 10; 
		}
		return res;
    }
}
{% endhighlight %}