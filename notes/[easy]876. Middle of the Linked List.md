# Middle of the Linked List
[Link](https://leetcode.com/problems/middle-of-the-linked-list/)

# Description

Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

# Example 1:

**Input**: [1,2,3,4,5]  
**Output**: Node 3 from this list (Serialization: [3,4,5])  
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).  
Note that we returned a ListNode object ans, such that:  
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.

# Example 2:

**Input**: [1,2,3,4,5,6]  
**Output**: Node 4 from this list (Serialization: [4,5,6])  
Since the list has two middle nodes with values 3 and 4, we return the second one.

# analysis
中间元素的定位问题  
* 对于数组，可以使用 (startInde + endIndex) / 2 定位；
* 对于链表，可以使用快慢指针，快指针每次前进两步，慢指针每次前进一步，当快指针到达尾部时，慢指针到达中间节点（slowDistance * 2 = fastDistance);
# Solution

    /**
     * Definition for singly-linked list.
     * public class ListNode {
     *     int val;
     *     ListNode next;
     *     ListNode(int x) { val = x; }
     * }
     */
    class Solution {
        public ListNode middleNode(ListNode head) {
            ListNode fast = head, slow = head;
            while (null != fast && null != fast.next) {
                fast = fast.next.next;
                slow = slow.next;
            }

            return slow;

        }
    }
