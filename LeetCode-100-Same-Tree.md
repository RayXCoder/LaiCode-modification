# 100. Same Tree

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

![100-1](images/100-same-tree-1.png)
![100-2](images/100-same-tree-2.png)

TC: O(n)

SC: O(logn)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null){
            return true;
        }
        
        if(p == null || q == null){
            return false;
        }
        
        if(p.val != q.val){
            return false;
        }
        
        boolean left = isSameTree(p.left, q.left);
        boolean right = isSameTree(p.right, q.right);
        
        return left && right;
        
    }
}
```
