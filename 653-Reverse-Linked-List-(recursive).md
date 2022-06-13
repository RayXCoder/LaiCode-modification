# 653. Reverse Linked List (recursive)

Reverse a singly-linked list recursively.

## Examples
+ L = null, return null
+ L = 1 -> null, return 1 -> null
+ L = 1 -> 2 -> 3 -> null, return 3 -> 2 -> 1 -> null

TC: O(n)

SC: O(n)

```java
/**
 * class ListNode { 
 *   public int value;
 *   public ListNode next;
 *   public ListNode(int value) {
 *     this.value = value;
 *     next = null;
 *   }
 * }
 */
public class Solution {
  public ListNode reverse(ListNode head) {
    // Write your solution here
    if(head == null || head.next == null){
      return head;
    }
    
    ListNode newHead = reverse(head.next);
    head.next.next = head;
    head.next = null;

    return newHead;
  }
}

```
