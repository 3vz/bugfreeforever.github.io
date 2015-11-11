---
layout: post
title:  Longest Substring Without Repeating Characters
author: Zhen Zhao
date:   2015-07-01 13:18:43 -05:00
categories: String
---
Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

### Clarify:
1. How to deal with space.

### Solution:
{% highlight java %}
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s == null)
            return 0;
        if(s.length() == 0)
            return 0;
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        int max = 1;
        int start = 0;
        for(int i = 0; i < s.length(); i++) {
            if(map.containsKey(s.charAt(i)) && map.get(s.charAt(i)) >= start) {
                start = map.get(s.charAt(i)) + 1;
                map.put(s.charAt(i), i);
            }
            else {
                map.put(s.charAt(i), i);
                max = Math.max(max, i - start + 1);
            }
        }
        return max;
    }
}
{% endhighlight %}