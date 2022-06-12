# 90. Subsets II

Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

 
## Example:
+ Example 1:

Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

+ Example 2:

Input: nums = [0]
Output: [[],[0]]
 

## Constraints:
+ 1 <= nums.length <= 10
+ -10 <= nums[i] <= 10

TC: O(2^n)

SC；O(n)

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        Arrays.sort(nums); //防止出现无序数列，为去重做准备 例如：（4  4 1 4 3，所以必须这么做来去重
        dfs(result, cur, nums, 0);
        return result;
    }
    
    private void dfs(List<List<Integer>> result, List<Integer> cur, int[] nums, int index){
        if(index == nums.length){
            result.add(new ArrayList<>(cur));
            return;
        }
        
        
        cur.add(nums[index]);
        dfs(result, cur, nums, index + 1);
        cur.remove(cur.size() - 1);
        
        while(index < nums.length - 1 && nums[index] == nums[index + 1]){ 
            //去重。为了防止出现重复数列，
            //所以在走‘没吃’之前检查下一个元素是相同，如果相同就不用走了直接跳过
            index++;
        }
        dfs(result, cur, nums, index + 1);
    }
}
```
