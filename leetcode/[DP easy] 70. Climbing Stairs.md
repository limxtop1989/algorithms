# Title: 70. Climbing Stairs
[Link](https://leetcode.com/problems/climbing-stairs/)

# Description
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:

    Input: 2
    Output: 2
    Explanation: There are two ways to climb to the top.
    1. 1 step + 1 step
    2. 2 steps

Example 2:

    Input: 3
    Output: 3
    Explanation: There are three ways to climb to the top.
    1. 1 step + 1 step + 1 step
    2. 1 step + 2 steps
    3. 2 steps + 1 step

# Solution in Java
    class Solution {

        public int climbStairs(int n) {
            if (n < 1) {
                return 0;
            } else if (n == 1) {
                return 1;
            } else if (n == 2) {
                return 2;
            }
            int[] table = new int[n + 1];
            table[1] = 1;
            table[2] = 2;
            return climb(n, table);
        }

        private int climb(int n, int[] table) {
            if (table[n] > 0) {
                // Use look up table, otherwise time limit exceeded. 
                return table[n];
            } else {
                // To reach nth step, stand n - 1th stair case and take 1 step,
                // or stand n - 2th stair case and take 2 steps. Both count 1
                // way respectively.
                int result = climb(n -1, table) + climb(n - 2, table);
                table[n] = result;
                return result;
            }
        }
    }
    
1 2 3 4 5 6  
1 2 3 5 8 13  
This is a Fabonacci sequence actully.
