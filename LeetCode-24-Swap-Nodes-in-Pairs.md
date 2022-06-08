# 24. Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

![24](images/24-Swap-In-Pairs.png)

TC: O(n)
 
SC: O(n)
 
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
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        
            ListNode first = head;
            ListNode second = head.next;
            
            
            first.next = swapPairs(head.next.next);
            second.next = first;
            
            
            return second;
        
        
    }
}
```
