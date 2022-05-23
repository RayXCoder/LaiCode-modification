# 66. All Valid Permutations Of Parentheses I
66-All-Valid-Permutations-Of-Parentheses-I.md

Given N pairs of parentheses “()”, return a list with all the valid permutations.

## Assumptions

N > 0
## Examples
+ N = 1, all valid permutations are ["()"]
+ N = 3, all valid permutations are ["((()))", "(()())", "(())()", "()(())", "()()()"]

TC: O(2^2k);
SC: O(2K);

```java

public class Solution {
 public List<String> validParentheses(int n) {
   // Write your solution here
   List<String> result = new ArrayList<>();
   char[] cur = new char[2*n];
   helper(result, cur, 0, n, n);
   return result;
 }
 
 private void helper(List<String> result, char[] cur, int index, int left, int right){
  //也可使用if(index = cur.length)
  //bug： 但 index 不等于 cur.length - 1
   if(left == 0 && right == 0){
     result.add(new String(cur));
     return;
   }
 
   if(left > 0){ 
     cur[index] = '(';  //01/25/2022: error: cur.add('(');
     helper(result, cur, index + 1, left - 1, right);
   }
                    
   if(right > left){ //01/24/2022：写成：left > 0
                     //01/25/2022: error: using elseif
                     //01/26/20222: error: right < left
 
     cur[index] = ')'; //01/25/2022: error: cur.add(')');
     helper(result, cur, index + 1, left, right - 1); 
     //01/24/2022: 忘记index+1；
   }
 }
}
