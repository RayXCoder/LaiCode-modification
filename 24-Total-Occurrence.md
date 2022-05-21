#24. Total Occurrence

Given a target integer T and an integer array A sorted in ascending order, Find the total number of occurrences of T in A.

## Examples
+ A = {1, 2, 3, 4, 5}, T = 3, return 1
+ A = {1, 2, 2, 2, 3}, T = 2, return 3
+ A = {1, 2, 2, 2, 3}, T = 4, return 0

## Corner Cases
+ What if A is null? We should return 0 in this case.

```java
public class Solution {
  public int totalOccurrence(int[] array, int target) {
    // Write your solution here
    if(array == null || array.length == 0){
      return 0;
    }

    return findByMergeSort(array, target, 0, 0, array.length - 1);
  }

  private int findByMergeSort(int[] array, int target, int count, int left, int right){
    if(left == right){
      if(array[left] == target){
        return 1;
      }
      return 0;
    }

    int mid = left + (right - left) / 2;
    int leftCheck = findByMergeSort(array, target, count, left, mid);
    int rightCheck = findByMergeSort(array, target, count, mid + 1, right);

    return leftCheck + rightCheck;
  }
}
