# 183. 2 Sum Closest

Find the pair of elements in a given array that sum to a value that is closest to the given target number. Return the values of the two numbers.

## Assumptions
+ The given array is not null and has length of at least 2

## Examples
+ A = {1, 4, 7, 13}, target = 7, closest pair is 1 + 7 = 8, return [1, 7].

TC: O(nlogn)
SC: O(n)

```java
public class Solution {
  public List<Integer> closest(int[] array, int target) {
    // Write your solution here
    List<Integer> result = new ArrayList<>();
    if(array == null || array.length == 0){
      return result;
    }
    Arrays.sort(array);
    
    if(array.length == 2){
     
      //result.addAll(Arrays.asList(array));
      result.add(array[0]);
      result.add(array[1]);
      return result;
    }

    int left = 0;
    int right = array.length - 1;
    int minDiff = Integer.MAX_VALUE;
    while(left < right){
      int sum = array[left] + array[right];
      int dif = Math.abs(sum - target);

      if(dif == 0){
        result.removeAll(result);
        result.add(array[left]);
        result.add(array[right]);
        return result;
      }
      
      if(dif < minDiff){
        minDiff = dif;
        result.removeAll(result);
        result.add(array[left]);
        result.add(array[right]);
      }

      if(sum > target){
        right--;
      }else{
        left++;
      }
    }

    return result;
  }
}
