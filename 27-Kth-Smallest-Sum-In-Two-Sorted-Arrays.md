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

TC: O(mn)
SC: O(mn)

## my consideration:
+ In this questions, we need to use a xy-coordinator to check and look for the k-th smallest number.
+ First of all, we need to find the initl point (x, y) = (0, 0). \ The 2nd smallest sum would be (x + 1, y) = (1, 0) or  (x, y + 1) = (0, 1). \ It is impossible to be (x + 1, y + 1) = (0, 1)


  
```
