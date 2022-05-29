# 201. Largest Container

Given an array of non-negative integers, each of them representing the height of a board perpendicular to the horizontal line, the distance between any two adjacent boards is 1. Consider selecting two boards such that together with the horizontal line they form a container. Find the volume of the largest such container.

## Assumptions
+ The given array is not null and has size of at least 2

## Examples
+ { 2, 1, 3, 1, 2, 1 }, the largest container is formed by the two boards of height 2, the volume of the container is 2 * 4 = 8.

TC: O(n)

SC: O(1)

```java
public class Solution {
  public int largest(int[] array) {
    // Write your solution here
    int left = 0;
    int right = array.length - 1;
    int maxContain = Integer.MIN_VALUE;

    while(left <= right){
      if(array[left] > array[right]){ //通过比较来判断哪边为高
        maxContain = Math.max(maxContain, array[right]*(right - left));
        right--;
      }else{
        maxContain = Math.max(maxContain, array[left]*(right - left));
        left++;
      }
    }

    return maxContain;
  }
}
