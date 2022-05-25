# 399. Rainbow Sort II

Given an array of balls, where the color of the balls can only be Red, Green, Blue or Black, sort the balls such that all balls with same color are grouped together and from left to right the order is Red->Green->Blue->Black. (Red is denoted by 0, Green is denoted by 1,  Blue is denoted by 2 and Black is denoted by 3).

## Examples
+ {0} is sorted to {0}
+ {1, 0} is sorted to {0, 1}
+ {1, 3, 1, 2, 0} is sorted to {0, 1, 1, 2, 3}

## Assumptions
+ The input array is not null.

```java

public class Solution {
  public int[] rainbowSortII(int[] array) {
    // Write your solution here
    if(array == null || array.length <= 1){
      return array;
    }

    int i = 0;
    int j = 0;
    int k = 0;
    int l = array.length - 1;

    // i左边不包含i: 存0
    // [i, j): 存1
    // [j,k]: unknown
    // (k, l]: 存2
    // l以后不包含l: 存3

    while(k <= l){
      if(array[k] == 0){
        swap(array, j, k++);
        swap(array, i++, j++);
      }else if(array[k] == 1){
        swap(array, j++, k++);
      }else if(array[k] == 2){
        k++;
      }else{
        swap(array, k, l--);
      }
    }

    return array;
  }

  private void swap(int[] array, int left, int right){
    int temp = array[left];
    array[left] = array[right];
    array[right] = temp;
  }
}
