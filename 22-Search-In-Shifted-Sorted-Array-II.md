#22. Search In Shifted Sorted Array II

Given a target integer T and an integer array A, A is sorted in ascending order first, then shifted by an arbitrary number of positions.

For Example, A = {3, 4, 5, 1, 2} (shifted left by 2 positions). Find the index i such that A[i] == T or return -1 if there is no such index.

##Assumptions

There could be duplicate elements in the array.
Return the smallest index if target has multiple occurrence. 
Examples

+ A = {3, 4, 5, 1, 2}, T = 4, return 1
+ A = {3, 3, 3, 1, 3}, T = 1, return 3
+ A = {3, 1, 3, 3, 3}, T = 1, return 1

##Corner Cases
What if A is null or A is of zero length? We should return -1 in this case.

```java
public class Solution {
  public int search(int[] array, int target) {
    // Write your solution here
    if(array == null || array.length == 0){
      return -1;
    }

    int left = 0;
    int right = array.length - 1;

    while(left < right - 1){
      int mid = left + (right - left) / 2;

      if(array[left] == target){
        right = left;
      }else if(array[mid] == target){
        right = mid;
      }else if(array[mid] > array[left] || array[mid] > array[right]){
        if(array[left] <= target && target <= array[mid]){
          right = mid ;
        }else{
          left = mid ;
        }
      }else if(array[mid] < array[left] || array[mid] < array[right]){

        if(array[mid] <= target && target <= array[right]){
          left = mid ;
        }else{
          right = mid ;
        }

      }else{
        right--;//如果相等：mid == left, 那我认为就应该--；
      }
    }

    if(array[left] == target){
      return left;
    }
    if(array[right] == target){
      return right;
    }

    return -1;
    
  }
}
