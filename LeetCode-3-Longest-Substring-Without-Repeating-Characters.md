# 3. Longest Substring Without Repeating Characters
3-Longest-Substring-Without-Repeating-Characters.md

Given a string s, find the length of the longest substring without repeating characters.

 

## Example:

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 

## Constraints:

0 <= s.length <= 5 * 104
s consists of English letters, digits, symbols and spaces.

## Method 1 - DP (This method would caused --- Time Limited Exceeded in extreme situation)
```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        if(s == null || s.length() == 0){
            return 0;
        }
        
        if(s.length() == 1){
            return 1;
        }

        int res = 0;
        for (int i = 1; i < n; i++) {
            for (int j = 0; j <= i; j++) {
                if (checkRepetition(s, i, j)) {
                    res = Math.max(res, i - j + 1);
                }
            }
        }

        return res;
    }

    private boolean checkRepetition(String s, int end, int start) {
        int[] chars = new int[128];

        for (int i = start; i <= end; i++) {
            char c = s.charAt(i);
            chars[c]++;
            if (chars[c] > 1) {
                return false;
            }
        }

        return true;
    }
}


## Method 2

