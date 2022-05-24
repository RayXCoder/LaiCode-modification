# 652. Common Numbers Of Two Sorted Arrays(Array version)
652-Common-Numbers-Of-Two-Sorted-Arrays(Array-version).md

Find all numbers that appear in both of two sorted arrays (the two arrays are all sorted in ascending order).

## Assumptions
+ In each of the two sorted arrays, there could be duplicate numbers.
+ Both two arrays are not null.

## Examples
+ A = {1, 1, 2, 2, 3}, B = {1, 1, 2, 5, 6}, common numbers are [1, 1, 2]

TC: O(m + n)

SC: O(min(m, n))

```java
public class Solution {
  public List<Integer> common(int[] A, int[] B) {
    // Write your solution here
   List<Integer> common = new ArrayList<>();
   
   int i = 0;
   int j = 0;
   while(i < A.length && j < B.length){
     if(A[i] == B[j]){
       common.add(A[i]);
       i++;
       j++;
     }else if(A[i] > B[j]){
       j++;
     }else{
       i++;
     }
   }

   return common;
  }
}
