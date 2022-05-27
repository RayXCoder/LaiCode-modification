# 2. Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Example:
Example 1:

Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]

Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]

## Constraints:
+ The number of nodes in each linked list is in the range [1, 100].
+ 0 <= Node.val <= 9
+ It is guaranteed that the list represents a number that does not have leading zeros.

TC: O(max(m, n)) //m, n are the length of the 2 listNodes

SC: O(max(m, n)) //m, n are the length of the 2 listNodes

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        
        ListNode a = l1;
        ListNode b = l2;
        ListNode cur = dummy;
        int term = 0;
        
        while(a != null || b != null || term != 0){
            //int term = 0;如果把term设在这里就不能保存上一轮中当 a + b > 9时余下来的数字了。
            if(a != null){
                term += a.val;
                a = a.next;
            }
            
            if(b != null){
                term += b.val;
                b = b.next;
            }
            
            cur.next = new ListNode(term % 10);
            term = term / 10;
            cur = cur.next;
        }
        
        return dummy.next;
    }
}
