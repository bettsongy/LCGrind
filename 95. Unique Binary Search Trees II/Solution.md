###### tags:

Backtracking, Tree, Binary Tree

###### date:

08/05/2023

[leetcode link](https://leetcode.com/problems/unique-binary-search-trees-ii/)

## **Description**

Given an integer n, return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.

#### Example 1

Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]times.

#### Example 2

Input: n = 1
Output: [[1]]

#### Constraints

1 <= s.length, p.length <= 3 \* 104
s and p consist of lowercase English letters.

## **Solution**

### Approach 1:

##### Code:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<TreeNode> generateTrees(int n) {

        LinkedList<TreeNode> list = new LinkedList<>();
        if(n == 0){
            return list;
        }

        return build(1, n);

    }

    private List<TreeNode> build(int left, int right){
        List<TreeNode> list = new LinkedList<>();

        if(left > right){
            list.add(null);
            return list;
        }

        for(int i = left; i <= right; i ++){

            List<TreeNode> leftList = build(left, i -1);
            List<TreeNode> rightList = build(i + 1, right);

            for(TreeNode leftNode : leftList){
                for(TreeNode rightNode : rightList){
                    TreeNode root = new TreeNode(i);
                    root.left = leftNode;
                    root.right = rightNode;
                    list.add(root);
                }

            }

        }

        return list;

    }
}
```

##### Complexity:

The time complexity of solution is O(4^N / N^(1.5)) using the Catalan number. Here's the reasoning behind this:

The number of binary search trees with 'n' distinct elements is given by the nth Catalan number. The nth Catalan number is given by (2n choose n) / (n + 1) = 4^n / (n^(3/2) \* sqrt(pi)) (approx), for large n. The function that generates all unique BSTs would therefore have a time complexity of O(4^N / N^(1.5)) since it generates all possible trees.

The space complexity of the solution is O(N). The space complexity is equal to the maximum depth of the recursion, which is n in the worst case scenario. The additional space for storing the trees is not considered here, because they are the result of the function, not the intermediate recursive computation.

So the final complexity analysis would be:

Time complexity: O(4^N / N^(1.5))
Space complexity: O(N)

## **Reference**
