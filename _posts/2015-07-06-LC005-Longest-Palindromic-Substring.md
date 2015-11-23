---
layout: post
title:  Longest Palindromic Substring
author: Zhen Zhao
date:   2015-07-06 13:26:43 -05:00
categories: String
---
Given a string S, find the longest palindromic substring in S. 

You may assume that the maximum length of S is 1000, 

and there exists one unique longest palindromic substring.

### Clarify:

1. "" will return "";

### Solution 1:

We can use dynamic programming

1. Create a n * n table match[row][col], row is start index, colis the end index.
2. Init the table as following rules: 

		match[i][i] == true, single letter is always palindromic.
		match[i][i + 1], check whether connected 2 letters are same or not, which help
		for the even letters combination checking.

3. Check combination with different length.

{% highlight java %}
public class Solution {
  public String longestPalindrome(String s) {
    if(s.length() == 0 || s == null)
      return "";
    if(s.length() == 1)
      return s;
    int max = 0;
    int startIndex = 0;
    int n = s.length();
    //dp[i][j] weather the substring which start at i, end at j is palindrome.
    boolean[][] dp = new boolean[n][n];
    //When substring's length is 1, they are all palindrome.
    for(int i = 0; i < n; i++) {
      dp[i][i] = true;
    }
    //When substring's length is 2.
    for(int i = 0; i < n - 1; i++) {
      if(s.charAt(i) == s.charAt(i + 1)) {
        dp[i][i + 1] = true;
        max = 2;
        startIndex = i;
      }
    }
    for(int len = 3; len <= n; len++){
        for(int i = 0; i <= n - len; i++) {
          int j = i + len - 1;
          if(dp[i + 1][j - 1] && s.charAt(i) == s.charAt(j)){
            max = len;
            startIndex = i;
            dp[i][j] = true;
          }
        }
    }
    return s.substring(startIndex, startIndex + max);
  }
}
{% endhighlight %}