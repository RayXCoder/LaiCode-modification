# 69. Sqrt(x)

Given a non-negative integer x, compute and return the square root of x.

Since the return type is an integer, the decimal digits are truncated, and only the integer part of the result is returned.

Note: You are not allowed to use any built-in exponent function or operator, such as pow(x, 0.5) or x ** 0.5.

 
## Example
Example 1:

Input: x = 4
Output: 2
Example 2:

Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.
 

## Constraints:
+ 0 <= x <= 2^(31) - 1

TC: O(logN)

SC: O(1)

```java
class Solution {
    public int mySqrt(int x) {
        if(x <= 1){
            return x;
        }
        
        int left = 0;
        int right = x/2;
        
        while(left <= right){
            int pivot = left + (right - left) / 2;
            long num = (long)pivot * pivot;
            if(x == num){
                return pivot;
            }else if(x < num){
                right = pivot - 1;
            }else{
                left = pivot + 1;
            }
        }
        
        return right;
    }
}
```
