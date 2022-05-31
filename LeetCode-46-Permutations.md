# 46. Permutations
LeetCode-46-Permutations.md

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

## Example

Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Example 2:
Input: nums = [0,1]
Output: [[0,1],[1,0]]

Example 3:
Input: nums = [1]
Output: [[1]]
 

## Constraints:
+ 1 <= nums.length <= 6
+ -10 <= nums[i] <= 10
+ All the integers of nums are unique.

TC: O(n!)

SC: O(n)

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        
        helper(result, nums, 0);
        return result;
    }
    
    private void helper(List<List<Integer>> result, int[] nums, int index){
        if(index == nums.length){
            
            List<Integer> cur1 = new ArrayList<>();
            for(int num : nums){
                cur1.add(num);
            }
            
            result.add(new ArrayList<>(cur1));
            cur1.removeAll(cur1);
            return;
        }
        
       
        for(int i = index; i < nums.length; i++){
            swap(index, i, nums);
            helper(result, nums, index + 1);
            swap(index, i, nums);
        }
    }
    
    private void swap(int left, int right, int[] nums){
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
}
```
