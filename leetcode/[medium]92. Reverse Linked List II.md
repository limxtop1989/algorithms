
# Title: 92. Reverse Linked List II
[Link](https://leetcode.com/problems/reverse-linked-list-ii/)

# Description
Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

# Example:

    Input: 1->2->3->4->5->NULL, m = 2, n = 4
    Output: 1->4->3->2->5->NULL
    
# Analysis
对【m, n】区间的单链表反转，返回reverseLinkedList，并与前后两段链表进行衔接。为此，需要提前，纪录m 的prev & n的next节点。
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
        public ListNode reverseBetween(ListNode head, int m, int n) {
            ListNode mHead = head, nHead = head;
            int index = 1;
            while (index < m - 1) {
                mHead = mHead.next;
                nHead = nHead.next;
                index++;
            }
            while (index <= n) {
                nHead = nHead.next;
                index++;
            }
            ListNode next;
            if (m == 1) {
                next = reverseLinkedList(mHead, nHead);
                head = next;
            } else {
                next = reverseLinkedList(mHead.next, nHead);
                mHead.next = next;
            }

            while (null != mHead.next) {
                mHead = mHead.next;
            }
            mHead.next = nHead;
            return head;
        }

        private ListNode reverseLinkedList(ListNode head, ListNode nHead) {
            ListNode current = head;
            ListNode prev = null;
            while (null != current && current != nHead) {
                ListNode next = current.next;
                current.next = prev;
                prev = current;
                current = next;
            }
            return prev;
        }
    }
