# Title: 62. Unique Paths
[Link](https://leetcode.com/problems/unique-paths/)

# Description
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?


Above is a 7 x 3 grid. How many possible unique paths are there?

Note: m and n will be at most 100.

Example 1:

    Input: m = 3, n = 2
    Output: 3
    Explanation:
    From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
    1. Right -> Right -> Down
    2. Right -> Down -> Right
    3. Down -> Right -> Right

Example 2:

    Input: m = 7, n = 3
    Output: 28


# Solution in Java
    class Solution {
        public int uniquePaths(int m, int n) {

            if (m < 1 || n < 1) {
                return 0;
            } else if (m == 1) {
                return 1;
            } else if (n == 1) {
                return 1;
            }
            int[][] table = new int[m][n];
            table[0][0] = 0;
            table[0][1] = 1;
            table[1][0] = 1;

            return uniquePaths(m, n, table);

        }

        private int uniquePaths(int m, int n, int[][] table) {
            if (table[m - 1][n - 1] > 0) {
                return table[m - 1][n - 1];
            } else {
                int result = 0;
                if (m == 1) {
                    result = 1;//uniquePaths(m, n - 1, table);
                } else if (n == 1) {
                    result = 1;//uniquePaths(m - 1, n, table);
                } else {
                    result = uniquePaths(m - 1, n, table) + uniquePaths(m, n - 1, table);
                }

                table[m - 1][n -1] = result;
                return result;
            }
        }
    }
