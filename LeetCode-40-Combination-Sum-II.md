# 40. Combination Sum II

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

Note: The solution set must not contain duplicate combinations.

 
## Example:
+ Example 1:
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
+ Example 2:
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
 

## Constraints:
+ 1 <= candidates.length <= 100
+ 1 <= candidates[i] <= 50
+ 1 <= target <= 30

TC: O(2^N)

SC: O(n)

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        
        Arrays.sort(candidates);
        dfs(result, cur, candidates, target, 0);
        return result;
    }
    
    private void dfs(List<List<Integer>> result, List<Integer> cur, int[] candidates, int target, int index){
        if(target == 0){
            result.add(new ArrayList<Integer>(cur));
            return;
        }
        
        for(int i = index; i < candidates.length; ++i){
            if(i  > index && candidates[i] == candidates[i - 1]){
                continue;
            }
            if(target - candidates[i] < 0){
                break;
            }
            //吃
            cur.add(candidates[i]);
            dfs(result, cur, candidates, target - candidates[i], i + 1);//放错了一个index让我看错了半天
            //吐
            cur.remove(cur.size() - 1);
        }
    }
}
```
