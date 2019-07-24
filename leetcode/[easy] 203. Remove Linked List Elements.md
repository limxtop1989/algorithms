# Title: 203. Remove Linked List Elements
[Link](https://leetcode.com/problems/remove-linked-list-elements/)

# Description
Remove all elements from a linked list of integers that have value val.

Example:

    Input:  1->2->6->3->4->5->6, val = 6
    Output: 1->2->3->4->5
    
# Solution:
    /**
     * Definition for singly-linked list.
     * public class ListNode {
     *     int val;
     *     ListNode next;
     *     ListNode(int x) { val = x; }
     * }
     */
    class Solution {
        public ListNode removeElements(ListNode head, int val) {
            if (null == head) {
                return null;
            }
            ListNode current = head;
            ListNode prev = null, next = null;
            while (current != null) {
                next = current.next;

                if (current.val == val) {
                    if (current != head) {
                        prev.next = next; 
                        current = next;
                    } else {
                        head = head.next;
                        current = head;
                    }
                } else {

                    prev = current;
                    current = next;
                }
            }
            return head;

        }
    }
