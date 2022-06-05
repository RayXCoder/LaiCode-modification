LeetCode-94-Binary-Tree-Inorder-Traversal.md

Given the root of a binary tree, return the inorder traversal of its nodes' values.

![94](images/94-inOrder-Traversa.png)

Method 1: 
<br/>TC: O(n)
<br/>SC: O(n)

Method 2: 
<br/>TC: O(n)
<br/>SC: O(n)

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

## Method 2. Iterative

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
       List<Integer> result = new ArrayList<>();
        Deque<TreeNode> stack = new LinkedList<>();
        
        //stack.offerFirst(root);
        TreeNode cur = root;
        while(cur != null || !stack.isEmpty()){
            while(cur != null){//如果cur不指向null那就开始走这个循环
                stack.offerFirst(cur);
                cur = cur.left;
            } //走完左边
            
            //开始弹出并顺带代入右子树
            cur = stack.pollFirst();
            result.add(cur.val);
            cur = cur.right;
            
        }
        
        return result;
    }
}
```
