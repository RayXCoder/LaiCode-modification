# 28. Implement strStr()

Implement strStr().

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

## Example:
+ Example 1:
Input: haystack = "hello", needle = "ll"
Output: 2
+ Example 2:
Input: haystack = "aaaaa", needle = "bba"
Output: -1
 

## Constraints:
+ 1 <= haystack.length, needle.length <= 10^4
+ haystack and needle consist of only lowercase English characters.

TC: O(n)

SC: O(1)

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle == null || needle.length() == 0){
            return -1;
        }
        
       if(needle.length() > haystack.length()){
           return -1;
       }
        
      int n = haystack.length();
      int m = needle.length();
       
      int i = 0;
      int j = i + m;
        
      while(j <= n){//必须是小于等于，否则就无法应对极端情况，例如： haystack = 'a', needle = 'a'
          String sub = haystack.substring(i, j);
          
          if(sub.equals(needle)){
              return i;
          }
          
          i++;
          j++;
      }
        
     return -1;
    }
}
```
