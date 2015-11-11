---
layout: post
title:  Median of Two Sorted Arrays
author: Zhen Zhao
date:   2015-11-05 23:34:43 -05:00
categories: Array
---
There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

### Clarify:



### Solution:
{% highlight java %}
public class Solution {
    public double findMedianSortedArrays(int[] A, int[] B) {
        if((A.length+B.length)%2==1)
            //odd count elements, reuturn the median one.
            return helper(A,B,0,A.length-1,0,B.length-1,(A.length+B.length)/2+1);
        else
            //even count elements, return the average of two elements in middle.
            return (helper(A,B,0,A.length-1,0,B.length-1,(A.length+B.length)/2)
                + helper(A,B,0,A.length-1,0,B.length-1,(A.length+B.length)/2+1))/2.0;
    }
  /**
   * The function it to find the kth element of two arrays.
   * @param A
   * @param B
   * @param i  A's start index
   * @param i2 A's end index
   * @param j  B's start index
   * @param j2 B's end index
   * @param k  the kth element
   * @return
   */
    private int helper(int[] A, int[] B, int i, int i2, int j, int j2, int k){
        //length of array A's search range.
        int m = i2-i+1;
        //length of array B's search range.
        int n = j2-j+1;
        //Switch place when A has more elements than B.
        if(m>n)
            return helper(B,A,j,j2,i,i2,k);
        //A's search range already be 0, return median of B's search range
        if(m==0)
            return B[j+k-1];
        //Find the first element of two arrays.
        if(k==1)
            return Math.min(A[i],B[j]);
        /*How many elements in array A.
          if posA == m, means k/2 is greater than the search range of A.
          But we still cannot make sure whether the result in A or not.
        */
        int posA = Math.min(k/2,m);
        //How many elements in array B.
        int posB = k-posA;
        if(A[i+posA-1]==B[j+posB-1])
            return A[i+posA-1];
        //situation 1
        else if(A[i+posA-1]<B[j+posB-1])
            //A's start index update to i + posA -1, 
            //B's end index update to j + posB -1.
            return helper(A,B,i+posA,i2,j,j+posB-1,k-posA);
        //situation 2 & 3
        else
            return helper(A,B,i,i+posA-1,j+posB,j2,k-posB);
    }
  }

The number above $ sign is the posA and posB index, 
also the element be compared.

1. situation 1:
	 A: 3  5  7  9  11
	          $-------
   B:           8   10  12  14  16  18
                ---------$
   

2. situation 2:
   A:            8  10  12  14  15 
                 --------$
   B: 1  2  3  4   9  11 
               $--------

3. situation 3:
   A:            8  10  
                 ----$
   B: 1  2  3  4   9  11  12  14  15 
               $------------
    
{% endhighlight %}

