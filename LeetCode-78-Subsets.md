# 78. Subsets

Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

TC: O(N x 2^N)

SC: O(N)
 
## Example
+ Example 1:
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
+ Example 2:
Input: nums = [0]
Output: [[],[0]]
 

## Constraints:
+ 1 <= nums.length <= 10
+ -10 <= nums[i] <= 10
+ All the numbers of nums are unique.

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        
        helper(result, cur, nums, 0);
        return result;
    }
    
    private void helper(List<List<Integer>> result, List<Integer> cur, int[] nums, int index){
        if(index == nums.length){
            result.add(new ArrayList<Integer>(cur));
            return;
        }
        //不吃
        helper(result, cur, nums, index + 1);
        //吃
        cur.add(nums[index]);
        helper(result, cur, nums, index + 1);
        //吐
        cur.remove(cur.size() - 1);
    }
}
```
