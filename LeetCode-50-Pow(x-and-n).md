# LeetCode 50. Pow(x, n)

Implement pow(x, n), which calculates x raised to the power n (i.e., xn).

## Example:

Example 1:

Input: x = 2.00000, n = 10
Output: 1024.00000
Example 2:

Input: x = 2.10000, n = 3
Output: 9.26100
Example 3:

Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
 

## Constraints:

-100.0 < x < 100.0
-2^31 <= n <= 2^31-1
-10^4 <= x^n <= 10^4

TC: O(logn)

SC: O(logn)

```java
class Solution {
    public double myPow(double x, int n) {
        long N = n; //必须得用long, 因为有可能会遇到overflow的数字
                    //example x = 2.00000,  n = -2147483648
                    //int:  -2,147,483,648 (-2^31) to 2,147,483,647 ((2^31))-1).
        if(n < 0){
            x = 1/x;
            N = -N;
        }
        
        return findPow(x, N);
        
    }
    
    public double findPow(double x, long n){
         if(n == 0){
            return 1.0;
        }
        
        if(n == 1){
            return x;
        }
        
        double half = findPow(x, n/2);
        
        if(n % 2 == 1){
            return half * half * x;
        }else{
            return half * half;
        }
    }
}
