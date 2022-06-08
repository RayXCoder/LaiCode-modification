# 142. Binary Tree Diameter

Given a binary tree in which each node contains an integer number. The diameter is defined as the longest distance from one leaf node to another leaf node. The distance is the number of nodes on the path.

If there does not exist any such paths, return 0.

## Examples

    5

  /    \

2      11

     /    \

    6     14

The diameter of this tree is 4 (2 → 5 → 11 → 14)

TC：O(n);

SC: O(logn);

```java
/**
 * public class TreeNode {
 *   public int key;
 *   public TreeNode left;
 *   public TreeNode right;
 *   public TreeNode(int key) {
 *     this.key = key;
 *   }
 * }
 */
public class Solution {
  public int diameter(TreeNode root) {
    // Write your solution here
    int[] max = new int[1];

    findDiameterMax(root, max);

    return max[0];
  }

  private int findDiameterMax(TreeNode root, int[] max){
    if(root == null){
      return 0;
    }

    int left = findDiameterMax(root.left, max);
    int right = findDiameterMax(root.right, max);

    if(root.left != null && root.right != null){
      max[0] = Math.max(max[0], 1 + right + left);
    }

    return 1 + Math.max(left, right);
  }
}
```
