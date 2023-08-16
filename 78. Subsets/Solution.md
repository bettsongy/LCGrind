###### tags:

Array, Backtracking

###### date: 

8/16/2023

[leetcode link](https://leetcode.com/problems/subsets/)



## **Description**

Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

#### Example 1

Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

#### Example 2

Input: nums = [0]
Output: [[],[0]]
 

#### Constraints

Constraints:

1 <= nums.length <= 10
-10 <= nums[i] <= 10
All the numbers of nums are unique.

## **Solution**



### Approach 1: 

##### Code:

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new LinkedList<>(); 
        traversal(nums,new LinkedList<Integer>() ,res, 0);
        
        return res;   
    }
    private void traversal(int[] nums,List<Integer> list,List<List<Integer>> res, int index){
        res.add(new LinkedList<>(list));
        
        for(int i = index; i < nums.length; i ++){
            list.add(nums[i]);
            traversal(nums, list, res, i + 1);
            list.remove(list.size() - 1);
        }
        
        
        
    }
}
```

##### Complexity:
- Time: O(2^n) because we are iterating the each element exactly twice, once including it and once excluing it 
- Space: O(n) Since each recursive call adds an element to the list, the maximum depth of the recursion is 
n, where n is the length of the input array nums.


### Follow up: 
供参考 Follow up：找出数组的子集数量，对于每个子集，它需要满足条件：min(S) + max(S) < K，要求将时间复杂度降到O(n)。

#### Approach

```JAVA
import java.util.*;

public class SubsetCounter {
    
    public static int countValidSubsets(int[] nums, int K) {
        Arrays.sort(nums);
        int count = 0;
        int n = nums.length;
        
        for(int i = 0; i < n; i++) {
            int j = i;
            while(j < n && nums[i] + nums[j] < K) {
                j++;
            }
            // subtracting one to exclude the empty set
            count += (2 << (j - i)) - 1;
        }
        
        return count;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5};
        int K = 6;
        System.out.println(countValidSubsets(nums, K)); // This should print the number of valid subsets
    }
}

```

## **Reference**