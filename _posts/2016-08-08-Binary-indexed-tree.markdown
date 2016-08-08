---
layout: post
title:  "Talk about BIT"
date:   2016-07-29 +0800
categories: algorithm
---

# Binary indexed tree

This data structure is used to deal with the problem that when you given an array ordinary idea can not make the update and delete both constrain in O(n^2). When the array is very large you will cost a lot of time.

An efficient way is use binary indexed tree or segment tree, the advantage of binary indexed tree is that it use less space and very easy to impplement. There are four functions to write. Construct function, update function, getSum, sum range function. The index transform trick is index & -index when the index add the previous value it will go to the next tree node that should also add the same value, when you subtract the previous value it will get its parent node. 

Phase 1: initiate the BIT

Phase 2 Sum function that can get sum from specific node to the root.

Phase 3: Implement update and sum range function from previous function.


 Talk is cheap:
{% highlight java %}
int[] BITree;
    int[] nums;
    public NumArray(int[] nums) {
        this.nums = nums;
        BITree = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i++) {
            init(i, nums[i]);
        }
    }
    void init(int i, int val) {
        i = i + 1;
        while (i < BITree.length) {
            BITree[i] += val;
            i += (i & (-i));
        }
    }
    void update(int i, int val) {
        int diff = val - nums[i];
        nums[i] = val;
        init(i, diff);
    }

    public int sumRange(int i, int j) {
        return getSum(j) - getSum(i - 1);
    }
    public int getSum(int index) {
        int sum = 0;
        index++;
        while (index > 0) {
            sum += BITree[index];
            index -= index & (-index);
        }
        return sum;
    }
{% endhighlight %}
