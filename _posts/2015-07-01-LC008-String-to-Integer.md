---
layout: post
title:  String to Integer
author: Zhen Zhao
date:   2015-11-05 23:34:43 -05:00
categories: String
---
Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

Update (2015-02-10):
The signature of the C++ function had been updated. If you still see your function signature accepts a const char * argument, please click the reload button  to reset your code definition.

### Clarify:
1. mulspace, special characters, sign bit, 
2. overflow

### Solution:
{% highlight java %}
import org.junit.Test;

public class Solution {
    public int myAtoi(String str) {
        if(str == null || str.length() == 0)
            return 0;
        int res = 0;
        int sign = 1;
        boolean signed = false;
        for(int i = 0; i < str.length(); i++) {
            if(str.charAt(i) == ' ') {
                // "-1 23" is illegal.
                if(signed || res != 0)
                    return res;
                else
                    continue;
            }
            if(str.charAt(i) == '-' || str.charAt(i) == '+') {
                // "+-123" is illegal.
                if(signed)
                    return 0;
                else {
                    sign = str.charAt(i) == '-'? -1: 1;
                    signed = true;
                    continue;
                }
            }
            if(str.charAt(i) >= '0' && str.charAt(i) <= '9') {
                int tail  = Integer.parseInt(String.valueOf(str.charAt(i)));
                // attention: MAX_VALUE = 2147483647, MIN_VALUE = -2147483648.
                // "2147483648" will return MAX_VALUE
                // attention "-2147483648" will be ok.
                if(sign == -1) {
                    int temp = sign * Math.abs(res)*10 - tail;
                    if ((temp + tail)/10 != res || temp * sign < 0) {
                        return Integer.MIN_VALUE;
                    }
                    else
                        res = temp;
                }
                else {
                    int temp = res * 10 + tail;
                    // in java , when overflow, it will be min_value,
                    // when it take away the tail, it will be max_value.
                    // (temp - tail)/10 != res is for overflow situation.
                    if ((temp - tail)/10 != res || temp * sign < 0 ) {
                        return Integer.MAX_VALUE;
                    }
                    else
                        res = temp;
                }
            }
            // "-12a23" should return -12.
            else
                return res;
        }
        return res;
    }

    @Test
    public void test() {
        //System.out.println(myAtoi("-12 2"));
        //System.out.println(myAtoi("+-12"));
        //System.out.println(myAtoi("112a2"));
        //System.out.println(myAtoi("2147483648"));
        //System.out.println(myAtoi("-2147483649"));
        System.out.println(myAtoi("   10522545459"));

    }
}
{% endhighlight %}