# 3. Longest Substring Without Repeating Characters
LeetCode-3-Longest-Substring-Without-Repeating-Characters.md

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

TC: O(n^3)

SC: O(min(m, n)). We need O(k) space for checking a substring has no duplicate characters, where kk is the size of the Set. The size of the Set is upper bounded by the size of the string nn and the size of the charset/alphabet m.

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

```

## Method 2 --- DP --- sliding down

TC: O(2n) == O(n)

SC: O(min(m, n))

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] letters = new int[128];
        
        int left = 0;
        int right = 0;
        int res = 0;
        while(right < s.length()){
            
            char cur = s.charAt(right);
            letters[cur]++;//make a report for each letter or symbols to avoid the repetition
                           //and report the times of the letter occurance
            
            
            //必须使用while，毕竟不可能重复字母字符只在开头结尾，
            //所以必须使用while顺着检查right左边的字符直到left碰到和right相重复的字母字符。
            //example: p w w k e w
            while(letters[cur] > 1){
                char start = s.charAt(left);
                letters[start]--;
                left++;
            }
            //right: the end of the unique string
            //left: the start of the unique string
              
            res = Math.max(res, right - left + 1);
            right++;
        }
        
        return res;
    }
}


