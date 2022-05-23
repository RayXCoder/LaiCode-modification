# 27. Kth Smallest Sum In Two Sorted Arrays
Given two sorted arrays A and B, of sizes m and n respectively. 
Define s = a + b, where a is one element from A and b is one element from B. Find the Kth smallest s out of all possible s'.

## Assumptions

A is not null and A is not of zero length, so as B
K > 0 and K <= m * n

## Examples

A = {1, 3, 5}, B = {4, 8}
+ 1st smallest s is 1 + 4 = 5
+ 2nd smallest s is 3 + 4 = 7
+ 3rd, 4th smallest s are 9 (1 + 8, 4 + 5) 
+ 5th smallest s is 3 + 8 = 11

TC: O(klogk)
SC: O(k), 总共只用了k大小的空间

## my consideration:
+ In this questions, we need to use a xy-coordinator to check and look for the k-th smallest number.
+ First of all, we need to find the initl point (x, y) = (0, 0).
<br /> The 2nd smallest sum would be (x + 1, y) = (1, 0) or  (x, y + 1) = (0, 1).
<br /> It is impossible to be (x + 1, y + 1) = (0, 1) 
+ Thus, If (x, y) is the m smallest sum, (x + 1, y) or (x, y + 1) is the m + 1 smallest sum

所以我们可以得到一个推论，假如当前组合(x, y)是第m小的和，那么(x + 1, y)和(x, y + 1)也可能是第m+1小，至于到底是不是那得让小顶堆说了算。因此，我们用一个小顶堆来记录组合，按照元素和作为比较条件。每从堆顶拿出一个组合，把它对应的两个相邻的组合放入堆里。重复k-1次，这样堆顶就是和第k小的组合了。

  
```java
public class Solution {
  
  public int kthSum(int[] A, int[] B, int k) {
    // Write your solution here
    if(A == null || A.length == 0 || B == null || B.length == 0){
      return -1;
    }

    int m = A.length;
    int n = B.length;
    if(m*n < k){
      return -1;
    }

    PriorityQueue<comb> minHeap = new PriorityQueue<>(
      new Comparator<comb>(){
        @Override
        public int compare(comb a, comb b){
          return Integer.compare(A[a.x] + B[a.y], A[b.x] + B[b.y]);
        }
      }
    );

    boolean[][] visited = new boolean[m][n];

    visited[0][0] = true;
    minHeap.offer(new comb(0, 0));

    //做到第K次就是k-th smallest sum
    for(int i = 0; i < k - 1; i++){
      comb cur = minHeap.poll();
      //绝对不能用minHeap.peek()，因为这样会导致永远无法去除最小的值，那样吐出来的值永远会在最小值不变了
      //example:
      //Input: new int[]{1,3,5,8,9}, new int[]{2,3,4,7}, 2
      //expected:<4> but was:<3>

      //测定 m 小的值(x, y)
      int x = cur.x;
      int y = cur.y;

      //测定 m + 1小的值

      //塞入(x + 1, y)的sum
      if(x + 1 < m && !visited[x + 1][y]){
        minHeap.offer(new comb(x + 1, y));
        visited[x + 1][y] = true;
      }

      //塞入(x, y + 1)的sum
      if(y + 1 < n && !visited[x][y + 1]){
        minHeap.offer(new comb(x, y + 1));
        visited[x][y + 1] = true;
      }
    }

    comb result = minHeap.peek();
    return A[result.x] + B[result.y];
  }

  //用class来建立各个sum的坐标
  class comb{
    int x;
    int y;

    comb(int x, int y){
      this.x = x;
      this.y = y;
    }
  }
}
