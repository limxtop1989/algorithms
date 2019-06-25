# Title
[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

# Description
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:

Given binary tree [3,9,20,null,null,15,7],

       3
      / \
     9   20
        /  \
       15   7
   
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
# Solution
**TODO Find a better solution**

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
        public List<List<Integer>> levelOrder(TreeNode root) {

            List<List<Integer>> intss = new ArrayList<List<Integer>>();
            if (null == root) {
                return intss;
            }
            List<TreeNode> nodes = new ArrayList<TreeNode>();
            nodes.add(root);
            List<Integer> ints = new ArrayList<Integer>();
            for (TreeNode node: nodes) {
                ints.add(node.val);
            }
            intss.add(ints);
            List<TreeNode> next; 
            while (null != (next = levelOrder(nodes))) {
                ints = new ArrayList<Integer>();
                nodes.clear();
                for (TreeNode node: next) {
                    ints.add(node.val);
                    nodes.add(node);
                }
                intss.add(ints);

            }
            return intss;

        }

        private List<TreeNode> levelOrder(List<TreeNode> treeNodes) {
            List<TreeNode> nextLevel = new ArrayList<TreeNode>(treeNodes.size() * 2);
            for (TreeNode node : treeNodes) {
                if (null != node.left) {
                    nextLevel.add(node.left);
                }
                if (null != node.right) {
                    nextLevel.add(node.right);
                }
            }

            if (nextLevel.size() == 0) {
                return null;
            }

            return nextLevel;
        }
    }
