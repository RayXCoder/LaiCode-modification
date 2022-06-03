# 5. Longest Palindromic Substring

Given a string s, return the longest palindromic substring in s.

## Example:
+ Example 1:
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.

+ Example 2:
Input: s = "cbbd"
Output: "bb"
 

## Constraints:
+ 1 <= s.length <= 1000
+ s consist of only digits and English letters.

TC: O(n^2)

SC: O(n^2)

```java
class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        
        boolean[][] dp = new boolean[len][len];
        int result = 1;
        int curLen = 0;
        
        int start  = 0;
        int end =0;
        
         for(int i = 0; i < len; i++){
            dp[i][i] = true;
        }
        
        //必须先列后行，这样才可以避免走进死胡同
        //此题DP的基本规律是从右上到左下角dp[i][j] ==> dp[i + 1][j - 1].
        //如果先行后列则势必造成空虚导致出错。
        //example: a a a a
        //dp[0][3] --->  dp[1][2]，
        //如果先行后列，则dp[1][2]保持空白状态False，必然出错
        //如果先列后行，则dp[1][2]已经将状态改为True, 才能得出正确结果
        for(int j = 0; j < len; j++){
            for(int i = 0; i < j; i++){
                if(i == j){
                    dp[i][j] = true;
                }else{
                    //i代表开始，J 代表结尾，如果 j - i = end - start = 单词长度
                    //单词长度为1或2时则只需要比较i，j位置上的字母本身就行了
                    dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i <= 2 || dp[i + 1][j - 1]);
                    if(dp[i][j] == true){
                        curLen = j - i + 1;
                    
                        if(curLen > result){
                            result = curLen;
                            start = i;
                            end = j;
                        }
                    }
                }
            }
        }
        
        return s.substring(start, end + 1);
    }
}
```
