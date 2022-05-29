# 9. Palindrome Number
LeetCode-9-Palindrome-Number.md

Given an integer x, return true if x is palindrome integer.

An integer is a palindrome when it reads the same backward as forward.

For example, 121 is a palindrome while 123 is not.
 
## Example:

Example 1:

Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
Example 2:

Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
 

## Constraints:
+ -2^31 <= x <= 2^31 - 1

TC: O(logn)

SC: O(1)

```java
class Solution {
    public boolean isPalindrome(int x) {
        //negative number: x < 0;
        //the number in [1, 10]
        //the number that is number zero, and the number whose last digit is zero
        //example: 10, 120. 30, 5200
        if(x < 0 || ((x % 10 == 0) && x != 0)){
            return false;
        }
        
        int revertNumber = 0;
        
        while(x > revertNumber){
            revertNumber  = revertNumber * 10 + x % 10;
            x /= 10;
        }
        
        //x == revertNumber: the number that is like 1001
        //x == revertNumber / 10 ： such as 232
        return x == revertNumber || x == revertNumber / 10;
    
                    
    }
}
```
