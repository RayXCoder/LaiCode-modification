# 15. 3Sum
LeetCode-15-3Sum.md

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

 
## Example:
+ Example 1:
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]

+ Example 2:
Input: nums = []
Output: []

+ Example 3:
Input: nums = [0]
Output: []
 

## Constraints:
0 <= nums.length <= 3000
-10^5 <= nums[i] <= 10^5

TC: O(n^2)

SC: O(logn) to O(n)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        
        List<List<Integer>> result = new ArrayList<>();
        
        for(int i = 0; i < nums.length && nums[i] <= 0; i++){
            if(i == 0 || nums[i - 1] != nums[i]){
                twoSumII(nums, i, result);
            }
            
        }
        
        return result;    
    }
    
    private void twoSumII(int[] nums, int i, List<List<Integer>> result){
       int lo = i + 1; 
       int hi = nums.length - 1;
        
        while(lo < hi){
            int sum = nums[i] + nums[lo] + nums[hi];
            if(sum < 0){
                lo++;
            }else if(sum > 0){
                hi--;
            }else{
                result.add(Arrays.asList(nums[i], nums[lo++], nums[hi--]));
                while(lo < hi && nums[lo] == nums[lo - 1]){
                    lo++;
                }
            }
        }
    }
}
```
