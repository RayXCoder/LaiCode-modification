# 14. Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

 
## Example:

+ Example 1:
Input: strs = ["flower","flow","flight"]
Output: "fl"

+ Example 2:
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
 

## Constraints:

1 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] consists of only lower-case English letters.

TC: O(s), where S is the number of all characters in the array,

SC: O(mlogn). There is a memory overhead since we store recursive calls in the execution stack. There are nlogn recursive calls, each store need mm space to store the result, so space complexity is O(m⋅logn)

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        //corner case
        if(strs == null || strs.length == 0){
            return "";
        }
            return longestCommonPrefix(strs, 0, strs.length - 1); 
    }
    
    //A  B  C  D  E
    //L     M     R
    //A B C   D E
    //L M  R
    //A B   C
    
    private String longestCommonPrefix(String[] strs, int left, int right){
        //Base case
        if(left == right){
            return strs[left];
        }else{
            int mid = left + (right - left) / 2;
            String segmentA = longestCommonPrefix(strs, left, mid);
            String segmentB = longestCommonPrefix(strs, mid + 1, right);
            return compareToFindCommon(segmentA, segmentB);
        }
    }
    
    //compare betweeen two words
    private String compareToFindCommon(String wordA, String wordB){
        int minLength = Math.min(wordA.length(), wordB.length());
            for(int i = 0; i < minLength; i++){
                if(wordA.charAt(i) != wordB.charAt(i)){
                    return wordA.substring(0, i);
                }
            }
        
        return wordA.substring(0, minLength);
    }
}

```
