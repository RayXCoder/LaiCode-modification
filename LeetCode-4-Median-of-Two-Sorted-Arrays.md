# 4. Median of Two Sorted Arrays
LeetCode-4-Median-of-Two-Sorted-Arrays.md

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

 
## Example
+ Example 1:
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
+ Example 2:
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
 
TC: O(log(min(m, n))

SC: O(1)

## Constraints:
+ nums1.length == m
+ nums2.length == n
+ 0 <= m <= 1000
+ 0 <= n <= 1000
+ 1 <= m + n <= 2000
+ -10^6 <= nums1[i], nums2[i] <= 10^6

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        
        //1必须比2短
        if(nums1.length > nums2.length){
            int[] temp = nums1;
	        nums1 = nums2;
	        nums2 = temp;
        }
        
        //如果替换过后发现数组一是空心的，那就把数组二顶替数组一完成下方程序
        if(nums1 == null || nums1.length == 0){
          nums1 = nums2;
        }
        
        int m = nums1.length;
        int n = nums2.length;
        
        //在第一个数组（短数组）的[0, m]查找恰当的分割线
        //交叉规则：
        //i代表短数组中位线左边的数字index
        //i - 1代表短数组中位线右边边的数字index
        //j代表长数组中位线左边的数字index
        //j - 1代表长数组中位线右边边的数字index
        //nums1[i - 1] <= nums2[j] && nums2[j - 1] <= nums2[i]
  
        //两个数组之和后左边的元素必须比右边的多一个，因为int的特性，所以奇偶数一样
        int sizeLeft = (m + n + 1) / 2; 

        int left = 0;
        int right = m; //nums1.length - 1;

        while(left < right){
            int i = left + (right - left + 1) / 2; //为了防止在循环体内部执行到0这个下标
                                                    //防止i - 1越界
            int j = sizeLeft - i; //两个数组左边元素之和 - 数组1的左边元素之和

            if(nums1[i - 1] > nums2[j]){ //数组1的左边的元素数值 》数组2的右边的元素数值
                                         //证明分割线太靠右了
                     right = i - 1;      //下一轮：[left, i - 1]
            }else{
                left = i;    //下一轮： [i, right]
            }
        }

        int i = left;
        int j = sizeLeft - i;

        int nums1LeftMax = i == 0 ? Integer.MIN_VALUE : nums1[i - 1];
        int nums1RightMin = i == m ? Integer.MAX_VALUE : nums1[i];

        int nums2LeftMax = j == 0 ? Integer.MIN_VALUE : nums2[j - 1];
        int nums2RightMin = j == n ? Integer.MAX_VALUE : nums2[j];

        if((m + n) % 2 == 1){ //数组长度之和为奇数
            return Math.max(nums1LeftMax, nums2LeftMax);
		    //物理安排上，左边比右边多一个，所以在左边选一个最大的
        }else{ //数组长度之和为偶数
            return ((double)(Math.max(nums1LeftMax, nums2LeftMax) + Math.min(nums1RightMin, nums2RightMin)))/2;
        }
  }
}
```
