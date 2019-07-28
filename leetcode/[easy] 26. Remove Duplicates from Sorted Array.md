# Title: 26. Remove Duplicates from Sorted Array
[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

# Description
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

    Given nums = [1,1,2],

    Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

    It doesn't matter what you leave beyond the returned length.
Example 2:

    Given nums = [0,0,1,1,1,2,2,3,3,4],

    Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

    It doesn't matter what values are set beyond the returned length.
    
# Solution
    class Solution {
        public int removeDuplicates(int[] nums) {
            int endIndex = nums.length - 1;
            int i = 0;
            while (i < endIndex) {
                if (nums[i] == nums[i + 1]) {
                    int temp = nums[i + 1];
                    move(nums, i + 1);
                    nums[endIndex--] = temp;
                } else {
                    i++;
                }
            }
            return endIndex + 1;
        }

        private void move(int[] nums, int begin) {
            int length = nums.length;
            for (int i = begin; i < length - 1; i++) {
                nums[i] = nums[i + 1];
            }
        }
    }
