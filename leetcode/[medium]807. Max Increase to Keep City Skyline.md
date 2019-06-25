# Title
[807. Max Increase to Keep City Skyline](https://leetcode.com/problems/max-increase-to-keep-city-skyline/)

# Description
In a 2 dimensional array grid, each value grid[i][j] represents the height of a building located there. We are allowed to increase the height of any number of buildings, by any amount (the amounts can be different for different buildings). Height 0 is considered to be a building as well. 

At the end, the "skyline" when viewed from all four directions of the grid, i.e. top, bottom, left, and right, must be the same as the skyline of the original grid. A city's skyline is the outer contour of the rectangles formed by all the buildings when viewed from a distance. See the following example.

What is the maximum total sum that the height of the buildings can be increased?

Example:
  
  Input: grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]  
  Output: 35  
  Explanation:   
  The grid is:    
[[3, 0, 8, 4],   
 [2, 4, 5, 7],  
 [9, 2, 6, 3],  
 [0, 3, 1, 0] ]

  The skyline viewed from top or bottom is: [9, 4, 8, 7]
  The skyline viewed from left or right is: [8, 7, 9, 3]

  The grid after increasing the height of buildings without affecting skylines is:

  gridNew =  
    [[8, 4, 8, 7],  
     [7, 4, 7, 7],  
     [9, 4, 8, 7],  
     [3, 3, 3, 3] ] 

# Notes:

* 1 < grid.length = grid[0].length <= 50.
* All heights grid[i][j] are in the range [0, 100].
* All buildings in grid[i][j] occupy the entire grid cell: that is, they are a 1 x 1 x grid[i][j] rectangular prism.

# Analysis
The value of gridNew[i][j] should not larger than the min(largest value in row, largest value in column);

# Solution
    class Solution {
        public int maxIncreaseKeepingSkyline(int[][] grid) {
            int length = grid.length;
            int[] maxRow = new int[length];
            int[] maxColumn = new int[length];

            for (int row = 0; row < length; row++) {
                int max = 0;
                for (int column = 0; column < length; column++) {
                    max = Math.max(max, grid[row][column]);
                }
                maxRow[row] = max;
            }

            for (int column = 0; column < length; column++) {
                int max = 0;
                for (int row = 0; row < length; row++) {
                    max = Math.max(max, grid[row][column]);
                }
                maxColumn[column] = max;
            }

            int difference = 0;
            for (int row = 0; row < length; row++) {
                for (int column = 0; column < length; column++) {
                    difference += Math.min(maxRow[row], maxColumn[column]) - grid[row][column];
                }

            }
            return difference;
        }
    }
    
# Solution
    class Solution {
        public int maxIncreaseKeepingSkyline(int[][] grid) {
            int length = grid.length;
            int[] maxRow = new int[length];
            int[] maxColumn = new int[length];

            for (int row = 0; row < length; row++) {
                for (int column = 0; column < length; column++) {
                    maxRow[row] = Math.max(maxRow[row], grid[row][column]);
                    maxColumn[column] = Math.max(maxColumn[column], grid[row][column]);
                }

            }

            int difference = 0;
            for (int row = 0; row < length; row++) {
                for (int column = 0; column < length; column++) {
                    difference += Math.min(maxRow[row], maxColumn[column]) - grid[row][column];
                }

            }

            return difference;


        }
    }
