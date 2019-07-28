# Title: 153. Find Minimum in Rotated Sorted Array
[Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

# Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]).

Find the minimum element.

You may assume no duplicate exists in the array.

Example 1:

    Input: [3,4,5,1,2] 
    Output: 1
Example 2:

    Input: [4,5,6,7,0,1,2]
    Output: 0

# Solution in C

    int findMinRecursive(int* nums, int start, int end) {
        if (start == end) {
            return nums[start];
        }
        int mid = (start + end) >> 1;
        if (nums[mid] < nums[end]) {
            // if nums[mid] < nums[end], the the min should left at left, including the mid.
            return findMinRecursive(nums, start, mid);
        } else {
            // the min should left on the right, excluding the mid, because nums[mid] has been larger than end.
            return findMinRecursive(nums, mid + 1, end);
        }
    }

    int findMin(int* nums, int numsSize) {
        return findMinRecursive(nums, 0, numsSize - 1);

    }

