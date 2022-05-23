#62. All Subsets I

Given a set of characters represented by a String, return a list containing all subsets of the characters.

## Assumptions
There are no duplicate characters in the original set.

# Examples
+ Set = "abc", all the subsets are [“”, “a”, “ab”, “abc”, “ac”, “b”, “bc”, “c”]
+ Set = "", all the subsets are [""]
+ Set = null, all the subsets are [];

```java
public class Solution {
  public List<String> subSets(String set) {
    // Write your solution here.
    List<String> result = new ArrayList<>();
    if(set == null){
      return result;
    }

    StringBuilder sb = new StringBuilder();
    char[] array = set.toCharArray();
    helper(result, sb, array, 0);
    return result;
  }

  private void helper(List<String> result, StringBuilder sb, char[] array, int index){
    if(index == array.length){
      result.add(new String(sb));
      return;
    }

    //not add
    helper(result, sb, array, index + 1);
    //add
    helper(result, sb.append(array[index]), array, index + 1);
    //吐
    sb.deleteCharAt(sb.length()- 1);
  } 
}
