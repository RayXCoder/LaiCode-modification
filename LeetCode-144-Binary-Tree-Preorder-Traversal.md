# 144. Binary Tree Preorder Traversal

Given the root of a binary tree, return the preorder traversal of its nodes' values.

Implement an iterative, pre-order traversal of a given binary tree, return the list of keys of each node in the tree as it is pre-order traversed.

Examples

        5

      /    \

    3        8

  /   \        \

1      4        11

Pre-order traversal is [5, 3, 1, 4, 8, 11]

Corner Cases

What if the given binary tree is null? Return an empty list in this case.
How is the binary tree represented?

We use the level order traversal sequence with a special symbol "#" denoting the null node.

For Example:

The sequence [1, 2, 3, #, #, 4] represents the following binary tree:

    1

  /   \

 2     3

      /

    4

 
 ## Method 1 Iteration
 
 TC: O(n)
 SC: O(n)
 
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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        helper(result, root);
        return result;
    }
    
    private void helper(List<Integer> result, TreeNode root){
        if(root == null){
            return;
        }
        
        result.add(root.val);
        helper(result, root.left);
        helper(result, root.right);
    }
}
 ```

## Method 2. Iteration

TC: O(n)

SC: O(n)

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if(root == null){
            return result;
        }
    
        
       Deque<TreeNode> stack = new LinkedList<>();
        stack.offerFirst(root);
        
        while(!stack.isEmpty()){
            TreeNode cur = stack.pollFirst();
            
            if(cur.right != null){ //先检测右边
                stack.offerFirst(cur.right);
            }
            
            if(cur.left != null){ //再检测左边， 这是为了第一个弹出左边，符合，root, left, right的规律
                stack.offerFirst(cur.left);
            }
            
            result.add(cur.val);
        }
        
        return result;
    }
}
```
