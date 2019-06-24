
# Title
[Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

# Description
Given a singly linked list, determine if it is a palindrome.  

# Example 1:

    Input: 1->2
    Output: false
    
# Example 2:

    Input: 1->2->2->1
    Output: true
    
    
# Follow up
Could you do it in O(n) time and O(1) space?

Use left and right pointer and traverse to the left and right end at the same time.

* The number of nodes is even:   
    
    1->2->2->1   
    1<-2<-left; right->2->1

* The number of nodes is odd:  

    1->2->3->2->1    
    1<-2<-left; right->2->1

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
        public boolean isPalindrome(ListNode head) {
            if (null == head) {
                return true;
            }
            ListNode fast = head;
            ListNode slow = head;
            while (null != fast && null != fast.next) {
                fast = fast.next.next;
                slow = slow.next;
            }
            ListNode left = reverseList(head, slow);
            ListNode right;
            if (null == fast) {
               right = slow; 
            } else {
               right = slow.next;
            }

            while (null != left && null != right) {
                if (left.val != right.val) {
                    return false;
                }
                left = left.next;
                right = right.next;
            }

            return true;

        }


        public ListNode reverseList(ListNode head, ListNode end) {
            ListNode current = head, prev = null;
            while (null != current && current != end) {
                ListNode next = current.next;
                current.next = prev;
                prev = current;
                current = next;
            }

            return prev;

        }
    }
