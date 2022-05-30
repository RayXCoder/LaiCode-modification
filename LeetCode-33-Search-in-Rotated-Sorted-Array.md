# 33. Search in Rotated Sorted Array

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

## Example:
<br/>Example 1:
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

<br/>Example 2:
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1

<br/>Example 3:
Input: nums = [1], target = 0
Output: -1
 

## Constraints:
+ 1 <= nums.length <= 5000
+ -10^4 <= nums[i] <= 10^4
+ All values of nums are unique.
+ nums is an ascending array that is possibly rotated.
+ -10^4 <= target <= 10^4

## Consideration:
+ 1. use the mid to compare the left and right to cut the sequence of ascending sequence
+ 2. if the nums[mid] > nums[right], left --> mid is ascending, using the target to compare with the nums[left] and nums[mid] to sure the next left or right. 
<br/>if the nums[mid] < nums[right], mid --> right is ascending, using the target to compare with the nums[mid] and nums[right] to sure the next left or right.

TC: O(logn)

SC: O(1)

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        
        while(left < right - 1){
            int mid = left + (right - 1);
            
            if(target == nums[mid]){
                return mid;
            }else if(nums[mid] > nums[left]){
                if(nums[left] <= target && target < nums[mid]){
                    right = mid - 1;
                }else{
                    left = mid + 1;
                }
            }else{
                if(nums[mid] < target && target <= nums[right]){
                    left = mid + 1;
                }else{
                    right = mid - 1;
                }
            }
        }
        
        if(nums[left] == target){
            return left;
        }
        
        if(nums[right] == target){
            return right;
        }
        
        return -1;
        
    }
}
```
