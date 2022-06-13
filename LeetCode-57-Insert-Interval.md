# 57. Insert Interval

You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

## Example:
+ Example 1:

Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

+ Example 2:

Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
 

## Constraints:
+ 0 <= intervals.length <= 10^4
+ intervals[i].length == 2
+ 0 <= starti <= endi <= 10^5
+ intervals is sorted by starti in ascending order.
+ newInterval.length == 2
+ 0 <= start <= end <= 10^5

TC: O(N)

SC: O(N)

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        LinkedList<int[]> output = new LinkedList<>();
        
        //取出新区间的两个值
        int newStart = newInterval[0];
        int newEnd = newInterval[1];
        
        int idx = 0;
        int n = intervals.length; //rows of the matrix
        
        //发现比新区间小的区间确定部分区间[a, b]中， newStart > a
        while(idx < n && newStart > intervals[idx][0]){
            output.add(intervals[idx++]);
        }
        
        int[] interval = new int[2];
        
        //判定是否最后一个收录的区间[a, b]中，a < newStart < b
        if(output.isEmpty() || output.getLast()[1] < newStart){
            //如果 a < b < newStart
            //就把新区间直接加上去
            output.add(newInterval);
        }else{
            //如果 a < newStart < b
            //那就判断newEnd和b谁大然后来决定如何合并区间
            interval = output.removeLast();
            interval[1] = Math.max(interval[1], newEnd);
            output.add(interval);
        }
        
        //然后继续处理剩下的区间来判断是否合并
        while(idx < n){
            //取出一个目前未定的区间[start end]
            interval = intervals[idx++];
            int start = interval[0];
            int end = interval[1];
            
            //取出最后一个之前收录的区间[a b]
            //如果b < start
            //则独立加入新区间
            
            //如果 b > start
            //那么则通过比较（end, b)的大小来决定如何合并区间
            //如果end > b, 则重新加入[a， end]
            //如果end < b, 则重新加入[start， b]
            if(output.getLast()[1] < start){
                output.add(interval);
            }else{
                interval = output.removeLast();
                interval[1] = Math.max(interval[1], end);
                output.add(interval);
            }
        }
        
        return output.toArray(new int[output.size()][2]);//创造一个nx2的矩阵
    }
}
```
