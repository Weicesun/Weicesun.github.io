---
layout: post
title:  "Backpack problem"
date:   2016-10-07 +0800
categories: algorithm
---

# Just finished midterm exam. I want to share some idea about backpack problem.

The idea is not mine but these solutions are pretty clear.

## No.1

Given n items with size Ai, an integer m denotes the size of a backpack. How full you can fill this backpack?
{% highlight java %}
 public int backPack(int m, int[] A) {
        // write your code here
        int[][] dp = new int[A.length + 1][m + 1];
       for (int i = 1; i < dp.length; i++) {
           for (int j = 1; j < dp[0].length; j++) {
               dp[i][j] = dp[i - 1][j];
               if (j >= A[i - 1]) {
                   dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - A[i - 1]] + A[i - 1]);
               }
           }
       }
       return dp[dp.length - 1][dp[0].length - 1];
    }

{% endhighlight %}

## No.2

Given n items with size Ai and value Vi, and a backpack with size m. What's the maximum value can you put into the backpack?

{% highlight java %}
 public int backPackII(int m, int[] A, int V[]) {
        // write your code here
         int[][] dp = new int[A.length + 1][m + 1];
       for (int i = 1; i < dp.length; i++) {
           for (int j = 1; j < dp[0].length; j++) {
               dp[i][j] = dp[i - 1][j];
               if (j >= A[i - 1]) {
                   dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - A[i - 1]] + V[i - 1]);
               }
           }
       }
       return dp[dp.length - 1][dp[0].length - 1];
    }

{% endhighlight %}

## No.3

Given n kind of items with size Ai and value Vi( each item has an infinite number available) and a backpack with size m. What's the maximum value can you put into the backpack?

{% highlight java %}
 public int backPackIII(int[] A, int[] V, int m) {
        // Write your code here
          int[][] dp = new int[A.length + 1][m + 1];
       for (int i = 1; i < dp.length; i++) {
           for (int j = 1; j < dp[0].length; j++) {
               dp[i][j] = dp[i - 1][j];
               if (j >= A[i - 1]) {
                   dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - A[i - 1]] + V[i - 1]);
               }
           }
       }
       return dp[dp.length - 1][dp[0].length - 1];
    }

{% endhighlight %}

## No.4

Given n items with size nums[i] which an integer array and all positive numbers, no duplicates. An integer target denotes the size of a backpack. Find the number of possible fill the backpack.

Each item may be chosen unlimited number of times

{% highlight java %}
 public int backPackIV(int[] A, int m) {
        // Write your code here
           int[][] dp = new int[A.length + 1][m + 1];
           dp[0][0] = 1;
       for (int i = 1; i < dp.length; i++) {
           for (int j = 0; j < dp[0].length; j++) {
               dp[i][j] = dp[i - 1][j];
               if (j >= A[i - 1]) {
                   dp[i][j] = dp[i][j] + dp[i][j - A[i - 1]];
               }
           }
       }
       return dp[dp.length - 1][dp[0].length - 1];
    }

{% endhighlight %}

## No.5

Given n items with size nums[i] which an integer array and all positive numbers. An integer target denotes the size of a backpack. Find the number of possible fill the backpack.

Each item may only be used once


{% highlight java %}
 public int backPackV(int[] A, int m) {
        // Write your code here
           int[][] dp = new int[A.length + 1][m + 1];
           dp[0][0] = 1;
       for (int i = 1; i < dp.length; i++) {
           for (int j = 0; j < dp[0].length; j++) {
               dp[i][j] = dp[i - 1][j];
               if (j >= A[i - 1]) {
                   dp[i][j] = dp[i - 1][j] + dp[i - 1][j - A[i - 1]];
               }
           }
       }
       return dp[dp.length - 1][dp[0].length - 1];
    }

{% endhighlight %}


