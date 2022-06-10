# 67. Add Binary

Given two binary strings a and b, return their sum as a binary string.

 
## Example:
+ Example 1:

Input: a = "11", b = "1"
Output: "100"

+ Example 2:

Input: a = "1010", b = "1011"
Output: "10101"
 

## Constraints:
+ 1 <= a.length, b.length <= 10^4
+ a and b consist only of '0' or '1' characters.
+ Each string does not contain leading zeros except for the zero itself.

TC: O(N + M)

SC: O(max(N, M))

```java
class Solution {
    public String addBinary(String a, String b) {
        int n = a.length() - 1;
        int m = b.length() - 1;
        int carry = 0;
        StringBuilder sb = new StringBuilder();
        
        while(n > -1 || m > -1){
            if(n > -1 && a.charAt(n) == '1'){
                carry++;
            }
            
            
            if(m > -1 && b.charAt(m) == '1'){
                carry++;
            }
           
            
            if(carry == 1 ){
                sb.append('1');
                carry = 0;
               
            }else if(carry == 0){
                sb.append('0');
                carry = 0;
            }else if(carry == 2){
                sb.append('0');
                carry = 1;
            }else if(carry == 3){
                sb.append('1');
                carry = 1;
            }
           
            n--;
            m--;
        }
        
        if(carry == 1){
            sb.append('1');
        }
        
        sb.reverse();
        
        return sb.toString();
    }
}
```
