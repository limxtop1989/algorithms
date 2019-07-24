# Title: 283. Move Zeroes
[Link](https://leetcode.com/problems/move-zeroes/)

# Description
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

    Input: [0,1,0,3,12]
    Output: [1,3,12,0,0]

Note:

You must do this in-place without making a copy of the array.
Minimize the total number of operations.

# Solution
    class Solution {
        public void moveZeroes(int[] nums) {
            int i = 0, j = 0;
            int length = nums.length;

            while (j < length - 1) {
                if (nums[i] != 0) {
                    i++;
                    j++;
                }

                if (nums[j] == 0) {
                    j++;
                }

                if (j == length) {
                    break;
                }

                if (nums[i] == 0 && nums[j] != 0) {
                    int temp = nums[i];
                    nums[i] = nums[j];
                    nums[j] = temp;

                }   
            }
        }
    }
    
# Solution
    class Solution {
        public void moveZeroes(int[] nums) {
            int length = nums.length;
            int slow = 0;
            for (int fast = 0; fast < length; fast++) {
                if (nums[fast] != 0) {
                    nums[slow] = nums[fast];
                    slow++;
                }    
            }

            for (int i = slow; i < length; i++) {
                nums[i] = 0;
            }
        }
    }
