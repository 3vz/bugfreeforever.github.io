---
layout: post
title:  ZigZag Conversion
author: Zhen Zhao
date:   2015-07-01 23:34:43 -05:00
categories: String
---
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this:

P~~~A~~~H~~~N

A~P~L~S~I~I~G

Y~~~I~~~R

And then read line by line: "PAHNAPLSIIGYIR".

### Clarify:

### Solution:
{% highlight java %}
public class LC006_ZigZagConversion {
    public String convert(String s, int numRows) {
        if(s == null || s.length() == 0 || numRows <= 0)
            return "";
        if(numRows == 1)
            return s;
        StringBuilder res = new StringBuilder();
        int zig = 2 * numRows - 2;
        for(int i = 0; i < numRows; i++) {
            for(int j = i; j < s.length(); j += zig){
                res.append(s.charAt(j));
                if(i != 0 && i != numRows - 1 && j + zig - 2 * i < s.length()){
                    // j + zig - 2 * i : j + zig stands for the next pattern's same position, 
                    // 2 * i means we need ga back  2 * i positions.
                    //  input: 1,2,3,4,5,6,7,8,9,10,11,12,13
                    //
                    //  1           7           13
                    //  2       6   8       12
                    //  3   5       9   11
                    //  4           10
                    //
                    //  zig = 6, 2 -> 8,  between them, there shoud be a 6, 
                    // so we need go back 2 * i positions.res.append(s.charAt(j + zig - 2 * i));
                }
            }
        }
        return res.toString();
    }
}
{% endhighlight %}