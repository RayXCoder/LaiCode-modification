# 31. Next Permutation

A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

+ For example, for arr = [1,2,3], the following are considered permutations of arr: [1,2,3], [1,3,2], [3,1,2], [2,3,1].

The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

+ For example, the next permutation of arr = [1,2,3] is [1,3,2].
+ Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
+ While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.

Given an array of integers nums, find the next permutation of nums. The replacement must be in place and use only constant extra memory.

## Example:
+ Example 1:

Input: nums = [1,2,3]
Output: [1,3,2]

+ Example 2:

Input: nums = [3,2,1]
Output: [1,2,3]

+ Example 3:

Input: nums = [1,1,5]
Output: [1,5,1]
 

## Constraints:
+ 1 <= nums.length <= 100
+ 0 <= nums[i] <= 100

TC: O(n)

SC: O(1)

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        
        //find the decreasing order from the array until nums[i - 1] < nums[i]
        //         0 1 2 3 4 5 6 7 8
        //Example: 1 5 8 4 7 6 5 3 1
        while(i >= 0 && nums[i] >= nums[i + 1]){
            i--;
        }
        
        // k = index = 3
        int k = i;
        
        //find the number nums[j] that is just greater than nums[i]
        if(k >= 0){
            int j = nums.length - 1;
            while(nums[j] <= nums[k]){
                j--;
            }
        //swap the number to get the new array
        //         0 1 2 3 4 5 6 7 8
        //Example: 1 5 8 5 7 6 4 3 1
            swap(nums, k, j);
        }
        
        //To find the next permutation that is greater than the current prmutation,
        //we need to swap sub array;
        //         0 1 2 3 4 5 6 7 8
        //Example: 1 5 8 5 7 6 4 3 1
        //swap:
        //Example: 1 5 8 5 1 3 4 6 7
        reverse(nums, k + 1);
    }
    
    private void swap(int[] nums, int left, int right){
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
    
    private void reverse(int[] nums, int start){
        int left = start;
        int right = nums.length - 1;
        
        while(left < right){
            swap(nums, left, right);
            left++;
            right--;
        }
        
    }
}
```
