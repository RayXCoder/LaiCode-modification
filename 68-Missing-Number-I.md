# 68. Missing Number I

Given an integer array of size N - 1, containing all the numbers from 1 to N except one, find the missing number.

## Assumptions
The given array is not null, and N >= 1

## Examples
+ A = {2, 1, 4}, the missing number is 3
+ A = {1, 2, 3}, the missing number is 4
+ A = {}, the missing number is 1

```java
public class Solution {
  public int missing(int[] array) {
    // Write your solution here
    Set<Integer> cur = new HashSet();

    for(int s : array){
      cur.add(s);
    }

    for(int i = 1; i < array.length + 1; i++){
      if(!cur.contains(i)){
        return i;
      }
    }

    return array.length + 1;
  }
}
