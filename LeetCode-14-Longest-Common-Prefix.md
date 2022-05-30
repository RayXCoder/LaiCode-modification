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

SC: O(mlogn). There is a memory overhead since we store recursive calls in the execution stack. There are \log nlogn recursive calls, each store need mm space to store the result, so space complexity is O(m \cdot \log n)O(m⋅logn)

```java

```
