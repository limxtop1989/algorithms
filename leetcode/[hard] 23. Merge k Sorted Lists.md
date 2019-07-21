# Title: 23. Merge k Sorted Lists
[Link](https://leetcode.com/problems/merge-k-sorted-lists/)

# Description
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:

    Input:
    [
      1->4->5,
      1->3->4,
      2->6
    ]
    Output: 1->1->2->3->4->4->5->6


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
        public ListNode mergeKLists(ListNode[] lists) {
            if (null == lists || lists.length == 0) {
                return null;
            }

            return merge(lists, 0, lists.length - 1);
        }

        private ListNode merge(ListNode[] lists, int low, int high) {
            if (low >= high) {
                return lists[low];
            }
            int middle = (low + high) >> 1;
            ListNode left = merge(lists, low, middle);
            ListNode right = merge(lists, middle + 1, high);
            return merge(left, right);
        }

        private ListNode merge(ListNode left, ListNode right) {
            if (null == left && right == null) {
                return null;
            }
            ListNode head = null, tail = null;
            if (null == left) {
                head = tail = right;
                right = right.next;
                while (null != right) {
                    tail.next = right;
                    tail = right;
                    right = right.next;
                }
                return head;
            }
            if (null == right) {
                head = tail = left;
                left = left.next;
                while (null != left) {
                    tail.next = left;
                    tail = left;
                    left = left.next;
                }
                return head;
            }
            if (left.val < right.val) {
                head = tail = left;
                left = left.next;
            } else {
                head = tail = right;
                right = right.next;
            }
            while (left != null && right != null) {
                if (left.val < right.val) {
                    tail.next = left;
                    tail = left;
                    left = left.next;
                } else {
                    tail.next = right;
                    tail = right;
                    right = right.next;
                }
            }

            while (null != left) {
                tail.next = left;
                tail = left;
                left = left.next;
            }

            while (null != right) {
                tail.next = right;
                tail = right;
                right = right.next;
            }
            return head;
        }
    }
