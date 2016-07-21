---
layout: post
title:  "Binary Tree Traverse"
date:   2016-06-17 +0800
categories: algorithem
---
There are three ways to traverse a binary tree : inorder preorder postorder

In each way there are two different approaches recursion and iterate

I will show iterate way to do

#preorder

{% highlight ruby %}
 public ArrayList<Integer> preorderTraversal(TreeNode root) {
        
        ArrayList<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        if (root == null) {
            return result;
        }
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode temp = stack.pop();
            result.add(temp.val);
            if (temp.right != null)
            stack.push(temp.right);
            if (temp.left != null)
            stack.push(temp.left);
        }
        return result;
    }
{% endhighlight %}

#inorder

{% highlight ruby %}
 public ArrayList<Integer> inorderTraversal(TreeNode root) {
        
        Stack<TreeNode> stack = new Stack<TreeNode>();
        ArrayList<Integer> result = new ArrayList<Integer>();
        if (root == null){
            return result;
        }
        stack.push(root);
        while (!stack.isEmpty()){
           while (root.left != null) {
               stack.push(root.left);
               root = root.left;
           }
           TreeNode node = stack.pop();
           result.add(node.val);
           if (node.right != null) {
               root = node.right;
               stack.push(root);
           } 
           
        }
        return result;
        
    }
{% endhighlight %}

#postorder

{% highlight ruby %}
public ArrayList<Integer> postorderTraversal(TreeNode root) {
       
        Stack<TreeNode> stack = new Stack<TreeNode>();
        ArrayList<Integer> result = new ArrayList<Integer>();
        if (root == null){
            return result;
        }
        TreeNode pre = null;
        stack.push(root);
        while (!stack.isEmpty()){
           
           TreeNode node = stack.peek();
           if ((node.left == null && node.right == null) || (pre != null && (pre == node.left || node.right == pre))) {
               result.add(node.val);
               stack.pop();
               pre = node;
           } else {
               if (node.right != null) {
                stack.push(node.right);
                }
                if (node.left != null) {
                    stack.push(node.left);
                }
           }
           
        }
        return result;
    }
{% endhighlight %}

