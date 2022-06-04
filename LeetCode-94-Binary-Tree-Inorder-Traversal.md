LeetCode-94-Binary-Tree-Inorder-Traversal.md

Given the root of a binary tree, return the inorder traversal of its nodes' values.

![94](images/94-inOrder-Traversa.png)


## Method 1. Recursion

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
    public List<Integer> inorderTraversal(TreeNode root) {
       List<Integer> result = new ArrayList<>();
        
        helper(root, result);
        return result;
    }
    
    private void helper(TreeNode root, List<Integer> result){
         if(root == null){
            return;
        }
        
        helper(root.left, result);
        result.add(root.val);
        helper(root.right, result);
    }
}
```
