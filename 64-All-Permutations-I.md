# 64. All Permutations I

Given a string with no duplicate characters, return a list with all permutations of the characters.
Assume that input string is not null.

## Examples
+ Set = “abc”, all permutations are [“abc”, “acb”, “bac”, “bca”, “cab”, “cba”]
+ Set = "", all permutations are [""]

TC: O(n!)

SC: O(n)

```java

public List<String> permutations(String input) {
  //solution:
  List<String> result = new ArrayList<>();
  if(input == null){
    return result;
  }
 
  char[] set = input.toCharArray();
  helper(set, result, 0);
  return result;
 }
 
 private void helper(char[] set, List<String> result, int index){
   if(index == set.length){ 
   //01/25/2022: my error：index == set.length - 1;
     result.add(new String(set)); //加入结果
     return;
   }
 
   for(int j = index; j < set.length; j++){ 
  //01/25/2022: my error：j = index + 1；
     swap(index, j, set); //吃
     helper(set, result, index + 1); //下一层
     swap(index, j, set); //吐
   }
 }
 
 private void swap(int i, int j, char[] sets){
   char temp = sets[i];
   sets[i] = sets[j];
   sets[j] = temp;
 }
}
