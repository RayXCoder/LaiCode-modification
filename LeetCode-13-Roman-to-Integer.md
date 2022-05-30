# 13. Roman to Integer

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:
+ I can be placed before V (5) and X (10) to make 4 and 9. 
+ X can be placed before L (50) and C (100) to make 40 and 90. 
+ C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

## Example:
<br/>Example 1:
Input: s = "III"
Output: 3
Explanation: III = 3.
<br/>Example 2:
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
<br/>Example 3:
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
 

## Constraints:
+ 1 <= s.length <= 15
+ s contains only the characters ('I', 'V', 'X', 'L', 'C', 'D', 'M').
+ It is guaranteed that s is a valid roman numeral in the range [1, 3999].

TC: O(1)

SC: O(1)

```java
class Solution {
   
    public int romanToInt(String s) {
        
        //用map将所需要的罗马数字归入一张hashMap
        Map<String, Integer> values = new HashMap<>();
    
        values.put("M", 1000);
        values.put("D", 500);
        values.put("C", 100);
        values.put("L", 50);
        values.put("X", 10); //掉了一个x,导致结果出错，所以必须仔细
        values.put("V", 5);
        values.put("I", 1);
    
        if(s == null || s.length() == 0){
            return 0;
        }
        
        
        int sum = 0;
        
        int i = 0;
        while(i < s.length()){
            //出去当前指针上的罗马数字
            String currentString = s.substring(i, i + 1);
            int currentValue = values.get(currentString);
            int nextValue = 0;
            
            //取出下一位的罗马数字
            if(i + 1 < s.length()){
                String nextString = s.substring(i + 1, i + 2);
                nextValue = values.get(nextString);
            }
            
            //检测当前字母以及下个字母是否组成了合适的罗马数字，例如：IX
            if(currentValue < nextValue){   //如果符合，得出这组罗马数字对应的数字
                sum += (nextValue - currentValue);
                i += 2;
            }else{                         //如果不符合，则只加当前的罗马数字对应的数字
                sum += currentValue;
                i += 1;
            }
        }
        
        return sum;
        
    }
}
```
