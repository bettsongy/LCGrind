###### tags:

LinkedList, Two Pointer

###### date:

08/05/2023

[leetcode link](https://leetcode.com/problems/partition-list/)

## **Description**

Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.



#### Example 1

Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]

#### Example 2

Input: head = [2,1], x = 2
Output: [1,2]

#### Constraints

The number of nodes in the list is in the range [0, 200].
-100 <= Node.val <= 100
-200 <= x <= 200
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
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode dummy1 = new ListNode(-1); 
        ListNode dummy2 = new ListNode(-1); 
        
        ListNode p1 = dummy1;
        ListNode p2 = dummy2; 
        while(head != null){
            
            if(head.val < x){
                p1.next = head; 
                p1 = p1.next; 
            }else{
                p2.next = head;
                p2 = p2.next;
            }
            
            ListNode temp = head.next; 
            head.next = null; 
            
            head = temp; 
            
        }
        
        p1.next = dummy2.next; 
        
        return dummy1.next; 
    }
}
```

##### Complexity:

- Time : we are iterating both linked list exactly once, so its O(m + n)

- Space : we are not creating any extra data strucuture that will grow with either linked list, so its O(1)
## **Reference**
