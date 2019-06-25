# Title
[111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

# Description
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

Example1:

    Given binary tree [3,9,20,null,null,15,7],

        3
       / \
      9  20
        /  \
       15   7
    return its minimum depth = 2.
 
 Example2:   
    Given binary tree [3,9],

        3
       /
      9
       
    return its minimum depth = 2.
    
    
# Analysis
TODO: Add figures here to illustrate.
* Case 1: There no children [min: 1, max: 1]     
* Case 2: There is only one child [min: 2, max: 2]  
* Case 3: Thre are two children [min: 2, max: 3]  

   
**Conclusion**  
If there is only one child, then the depth should be 1 + minDepth(child) rather than 1 + Math.min(minDepth(left), minDepth(right))

# Solution

    /**
     * Definition for a binary tree node.
     * public class TreeNode {
     *     int val;
     *     TreeNode left;
     *     TreeNode right;
     *     TreeNode(int x) { val = x; }
     * }
     */
    class Solution {
        public int minDepth(TreeNode root) {

            if (null == root) {
                return 0;
            }
            // TODO
            if (null == root.left) {
                return 1 + minDepth(root.right);
            } else if (null == root.right) {
                return 1 + minDepth(root.left);
            } else {
                return 1 + Math.min(minDepth(root.left), minDepth(root.right));   
            }
        }
    }
