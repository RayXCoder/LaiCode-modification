# 27. Remove Element
LeetCode-27-Remove-Element.md

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

![27-desription](images/27-remove-unique-element.png)

## Constraints:
+ 0 <= nums.length <= 100
+ 0 <= nums[i] <= 50
+ 0 <= val <= 100

TC；O(n)

SC: O(1)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0; //to count how many different elements in the array
        
        for(int j = 0; j < nums.length; j++){
            if(nums[j] != val){
                nums[i] = nums[j];
                i++;
            }
        }
        
        return i;
    }
}
```
