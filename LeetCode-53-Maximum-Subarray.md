# 53. Maximum Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

 
## Example:
+ Example 1:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.

+ Example 2:
Input: nums = [1]
Output: 1

+ Example 3:
Input: nums = [5,4,-1,7,8]
Output: 23
 

## Constraints:
+ 1 <= nums.length <= 10^5
+ -10^4 <= nums[i] <= 10^4

TC: O(n)

SC: O(1)

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int curSub = nums[0];
        int maxSub = nums[0];
        
        for(int i = 1; i < nums.length; i++){
            
            //比较过去以及pointer的值
            //物理意义上： curSub += nums[i];
            //如果curSub < current pointed (nums[i])就另起开头
            curSub = Math.max(nums[i], curSub + nums[i]);
            
            //maxSub储存最大的值
            maxSub = Math.max(curSub, maxSub);
        }
        
        return maxSub;
    }
}
```
