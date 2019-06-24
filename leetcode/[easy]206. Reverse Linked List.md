# Reverse a singly linked list
[Link](https://leetcode.com/problems/reverse-linked-list/)

# Description
Reverse a singly linked list.

# Example:

    Input: 1->2->3->4->5->NULL
    Output: 5->4->3->2->1->NULL

# Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

# Iterative Solution
    /**
     * Definition for singly-linked list.
     * public class ListNode {
     *     int val;
     *     ListNode next;
     *     ListNode(int x) { val = x; }
     * }
     */
    class Solution {
        public ListNode reverseList(ListNode head) {
            ListNode current = head, prev = null;
            while (null != current) {
                ListNode next = current.next;
                current.next = prev;
                prev = current;
                current = next;
            }

            return prev;

        }
    }
    
# Recursive Solution
    **Memory Limit Exceeded, but I don't figure out why**
    /**
     * Definition for singly-linked list.
     * public class ListNode {
     *     int val;
     *     ListNode next;
     *     ListNode(int x) { val = x; }
     * }
     */
    class Solution {
        public ListNode reverseList(ListNode head) {
            if (null == head.next) {
                return head;
            }

            //ListNode nextNode = head.next;
            ListNode newHead = reverseList(head.next);
            head.next.next = head;

            return newHead;

        }
    }
# Recursive Solution
    /**
     * Definition for singly-linked list.
     * public class ListNode {
     *     int val;
     *     ListNode next;
     *     ListNode(int x) { val = x; }
     * }
     */
    class Solution {
        public ListNode reverseList(ListNode head) {
            if (null == head) {
                return head;
            }
            return reverseList(null, head);
        }
        /**
         * Invariant variable:
         * 1. prev references the head node of reverse order linked list;
         * 2. head references the head node of the original order linked list;
         */
        private ListNode reverseList(ListNode prev, ListNode head) {
            if (head.next == null) {
                // we have reached the tail node, this is the new head node;
                head.next = prev;
                return head;
            }

            // Reference the next node first;
            ListNode next = head.next;
            // Reverse the link direction from next node to previous one;
            head.next = prev;

            return reverseList(head, next);
        }
    }
