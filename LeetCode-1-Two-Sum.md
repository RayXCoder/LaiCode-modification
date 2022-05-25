# LeetCode 1 Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 
## Example:

Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
 
## Constraints:

+ 2 <= nums.length <= 104
+ -109 <= nums[i] <= 109
+ -109 <= target <= 109
+ Only one valid answer exists.

## notes:
我使用了652的solution试图解决，但是发现不行，因为这个array不是sorted ascending，同时主义审题，这道题问的是index，而是直接的elements of the array.

TC: o(n)

SC: O(n)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        //HashMap <key, value>
        
            for(int i = 0; i < nums.length; i++){
            
                int complement = target - nums[i];
                if(map.containsKey(complement)){
                    return new int[]{i, map.get(complement)};
                    //不能这么用：eturn new int[]{i, map.get(complement)};
                    //这道题问的是对应的index，所以不能直接上交value，而是上交index of value
                }
                map.put(nums[i], i);
            }
        
        return null;
    }
}
