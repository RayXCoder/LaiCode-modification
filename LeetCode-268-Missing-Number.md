# 268. Missing Number

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

## Example:

<br />Example 1:
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
<br />Example 2:
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
<br />Example 3:
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
 

## Constraints:

+ n == nums.length
+ 1 <= n <= 104
+ 0 <= nums[i] <= n
+ All the numbers of nums are unique.

## Method 1. XOR ways
My consideration: By the discrete mathmatics --- Associative Laws A xor (B xor C) = (A xor B) xor C)

### Algorithm: 
Because we know that nums contains nn numbers and that it is missing exactly one number on the range [0..n-1], we know that nn definitely replaces the missing number in nums. Therefore, if we initialize an integer to nn and XOR it with every index and value, we will be left with the missing number. Consider the following example (the values have been sorted for intuitive convenience, but need not be):
![XOR ways](images/XORways.png)

TC: O(n)

SC: O(1)

```java
class Solution {
    public int missingNumber(int[] nums) {
        int missing = nums.length;
        
        for(int i = 0; i < nums.length; i++){
            missing ^= i ^ nums[i];
        }
        
        return missing;
        
    }
}
```

## Method 2. BFS ways

My consideration: I sued the ways from LaiOffer-69. It is related to BFS. But, it is slower than method 1 in the leetCode
TC: O(logn)

SC: O(1)

```java
class Solution {
    public int missingNumber(int[] nums) {
        int left = 0;
        int right = nums.length;
        
        Arrays.sort(nums);
        
        while(left < right){
            int mid = left + (right - left) / 2;
            if(nums[mid] == mid){ //???????????????????????? left???mid??????????????????????????????
                left = mid + 1;
            }else{ //????????????????????????left???mid?????????????????????????????????
                right = mid;
            }
        }
        
        return left;
        
    }
}
```
