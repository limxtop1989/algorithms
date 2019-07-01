# Title
[912. Sort an Array] (https://leetcode.com/problems/sort-an-array/)

# Description
Given an array of integers nums, sort the array in ascending order.

# Example 1:

    Input: [5,2,3,1]
    Output: [1,2,3,5]

# Example 2:

    Input: [5,1,1,2,0,0]
    Output: [0,0,1,1,2,5]
 

# Note:

* 1 <= A.length <= 10000
* -50000 <= A[i] <= 50000

# Solution
    class Solution {
        public int[] sortArray(int[] nums) {
            //quickSort(nums, 0, nums.length);
            //return insertSort(nums);
            //return selectSort(nums);
        }

        private void quickSort(int[] nums, int start, int end) {
            int diff = end - start;
            if (diff <= 12) {
                insertSort(nums, start, end);
                return;
            }

            int partition = partition(nums, start, end);
            quickSort(nums, start, partition - 1);
            quickSort(nums, partition + 1, end);
        }

        private int partition(int[] nums, int start, int end) {
            int less = start;
            for (int i = start; i <= end; i++) {
                if (isLess(nums, i, end)) {
                    exchange(nums, less, i);
                    less++;
                }
            }

            exchange(nums, less, end);
            return less;
        }

        private int[] insertSort(int[] nums, int start, int end) {
            for (int i = start; i <= end; i++) {
                for (int j = i; j > start && isLess(nums, j, j - 1); j--) {
                    exchange(nums, j, j - 1);
                }
            }

            return nums;
        }

        /**
         * First, find the smallest item in the array and exchange it with the first
         * entry. Then, find the next smallest item and exchange it with the second 
         * entry. Continue in this way, until the entire array is sorted. This method
         * is called selection sort because it works by repeatedly selecting the 
         * smallest remaining item.
         **/
        private int[] selectSort(int[] nums) {
            int length = nums.length;
            for (int i = 0; i < length - 1; i++) {
                int smallest = i;
                for (int j = i + 1; j < length; j++) {
                    if (nums[j] < nums[smallest]) {
                        smallest = j;
                    }
                }
                exchange(nums, i, smallest); 
            }
            return nums;
        }

        private void exchange(int[] nums, int i, int j) {
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
        /**
         * Insertion sort works the way many people sort a hand of playing cards. 
         * which starts with an empty left hand and the cards face down on the table. 
         * We remove one card at a time from the table and insert it into the correct
         * position in the left hand. To find the correct position for a card, we
         * compare it with each card in the hand, from right to left.
         */
        private int[] insertSort(int[] nums) {
            int length = nums.length;
            for (int i = 1; i < length; i++) {
                int key = nums[i];
                for (int j = i; j > 0 && isLess(nums, j, j - 1); j--) {
                    exchange(nums, j, j - 1);
                }
            }

            return nums;
        }

        private boolean isLess(int[] nums, int i, int j) {
            return nums[i] < nums[j];
        }
    }
