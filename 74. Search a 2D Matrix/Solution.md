###### tags:

Array, Binay Search

###### date: 

8/02/2023

[leetcode link](https://leetcode.com/problems/search-a-2d-matrix/)



## **Description**

You are given an m x n integer matrix matrix with the following two properties:

Each row is sorted in non-decreasing order.
The first integer of each row is greater than the last integer of the previous row.
Given an integer target, return true if target is in matrix or false otherwise.

You must write a solution in O(log(m * n)) time complexity.



#### Example 1

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true

#### Example 2

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false

 

#### Constraints

m == matrix.length
n == matrix[i].length
1 <= m, n <= 100
-104 <= matrix[i][j], target <= 104

## **Solution**



### Approach 1: 

##### Code:

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
    
        int left = 0;
        int right = matrix.length - 1;
        int m = matrix.length; 
        int n = matrix[0].length; 
        
        while(left <= right){
            int mid = left + (right - left) / 2; 
            if(target <= matrix[mid][n - 1] && target >= matrix[mid][0]){
                // this is the row
                int colLeft = 0;
                int colRight = n - 1; 
                while(colLeft <= colRight){
                    int colMid = colLeft + (colRight - colLeft) / 2; 
                    if(matrix[mid][colMid] == target){
                        return true; 
                    }else if(matrix[mid][colMid] > target){
                        colRight = colMid - 1; 
                    }else{
                        colLeft = colMid + 1; 
                    }              
                }
                return false; 
            }else if(target > matrix[mid][n - 1]){
                left = mid + 1; 
            }else{ // target < matrix[mid][0]
                right = mid - 1;
            }
        }
        return false;
    }
}
```

##### Complexity:
- Time: O(log(m) + log(n)) we are leveraging binary seach to traverse the row and column, so its O(log(m) + log(n)) 
- Space: O(1) we don't use any additional data structure so its constant

## **Reference**