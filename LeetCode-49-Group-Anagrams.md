# 49. Group Anagrams

LeetCode-49-Group-Anagrams.md

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 
## Example:
+ Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

= Example 2:
Input: strs = [""]
Output: [[""]]

+ Example 3:
Input: strs = ["a"]
Output: [["a"]]
 

## Constraints:
+ 1 <= strs.length <= 10^4
+ 0 <= strs[i].length <= 100
+ strs[i] consists of lowercase English letters.

TC: O(NKlogK)
+ where N is the length of strs, 
+ K is the maximum length of a string in strs. 
The outer loop has complexity O(N) as we iterate through each string. Then, we sort each string in O(KlogK) time.

SC: O(NK)

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if(strs.length == 0){
            return new ArrayList<>();
        }
            
            Map<String, List> result = new HashMap<String, List>();
            
            for(String s : strs){
                char[] ca = s.toCharArray();
                Arrays.sort(ca);
                String key = String.valueOf(ca);
                
                if(!result.containsKey(key)){
                    result.put(key, new ArrayList());
                }
                
                result.get(key).add(s);
            }
            
            return new ArrayList(result.values());
        
    }
}
```
