# 258. Move 0s To The End I

Given an array of integers, move all the 0s to the right end of the array.

The relative order of the elements in the original array does not need to be maintained.

## Assumptions:
+ The given array is not null.

## Examples:
+ {1} --> {1}
+ {1, 0, 3, 0, 1} --> {1, 3, 1, 0, 0} or {1, 1, 3, 0, 0} or {3, 1, 1, 0, 0}

TC: O(n)
SC: O(1)

```java
public class Solution {
  public int[] moveZero(int[] array) {
    // Write your solution here
    if(array == null || array.length <= 1){
      return array;
    }
    int left = 0;
    int right = array.length - 1;

    while(left < right){
      if(array[left] != 0){
        left++;
      }else if(array[right] == 0){
        right--;
      }else{
        swap(left, right, array);
        left++;
        right--;
      }
    }

    return array;
  }

  private void swap(int left, int right, int[] array){
    int temp = array[right];
    array[right] = array[left];
    array[left] = temp;
  }
}

```
