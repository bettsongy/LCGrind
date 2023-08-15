###### tags:

Array, BFS
 
###### date: 

8/15/2023

[leetcode link](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/)

## **Description**

You are given an m x n integer matrix grid where each cell is either 0 (empty) or 1 (obstacle). You can move up, down, left, or right from and to an empty cell in one step.

Return the minimum number of steps to walk from the upper left corner (0, 0) to the lower right corner (m - 1, n - 1) given that you can eliminate at most k obstacles. If it is not possible to find such walk return -1.

#### Example 1

Input: grid = [[0,0,0],[1,1,0],[0,0,0],[0,1,1],[0,0,0]], k = 1
Output: 6
Explanation: 
The shortest path without eliminating any obstacle is 10.
The shortest path with one obstacle elimination at position (3,2) is 6. Such path is (0,0) -> (0,1) -> (0,2) -> (1,2) -> (2,2) -> (3,2) -> (4,2).
#### Example 2

Input: grid = [[0,1,1],[1,1,1],[1,0,0]], k = 1
Output: -1
Explanation: We need to eliminate at least two obstacles to find such a walk.



#### Constraints


m == grid.length
n == grid[i].length
1 <= m, n <= 40
1 <= k <= m * n
grid[i][j] is either 0 or 1.
grid[0][0] == grid[m - 1][n - 1] == 0

## **Solution**



### Approach 1: 

For this approach, we are leveraging many techniques: 

1. BFS to compute the shortest distance
2. PriorityQueue and Heurustic to achieve a A* or Djistra algorithm
3. Leveraging a visited 3D array to keep track of which cell is visited before inserting it to our priority queue 

##### Code:

```java
class Cell implements Comparable<Cell>{ 
    public int steps, row, col, k, h; 

    
    public Cell(int steps, int row, int col, int k, int h){
        this.steps = steps; 
        this.row = row; 
        this.col = col; 
        this.k = k; 
        this.h = h; 
    } 
    @Override
    public int compareTo(Cell other){
        return Integer.compare(this.steps + this.h, other.steps + other.h);
    }
    
        
}
class Solution {
    
    int[][] dirs = new int[][]{{1,0}, {-1,0}, {0, 1}, {0, -1}}; 
  
    public int shortestPath(int[][] grid, int k) {
        
        
        int m = grid.length;
        int n = grid[0].length; 
        if(m - 1 == 0 && n - 1 == 0){
            return 0; 
        }
        boolean[][][] seen = new boolean[m][n][k + 1];
        PriorityQueue<Cell> q = new PriorityQueue<>();
        
        Cell start = new Cell(0, 0, 0, k, m + n - 2);
        
        q.offer(start);
        
        while(!q.isEmpty()){
            Cell cell = q.poll(); 
            for(int[] dir : dirs){
                
                int newRow = cell.row + dir[0];
                int newCol = cell.col + dir[1]; 
                int newK = cell.k;  
               
                if(newRow < 0 || newRow > m - 1 || newCol < 0 || newCol > n - 1) 
                {
                    continue; 
                }
                if(grid[newRow][newCol] == 1){
                    newK --; 
                }
                
                if(newK < 0 ){
                    continue; 
                }
                
                if(seen[newRow][newCol][newK]){
                    continue; 
                }
               
                if(newRow == m - 1 && newCol == n - 1){
                    return cell.steps + 1; 
                }
                int newStep = cell.steps + 1; 
                seen[newRow][newCol][newK] = true; 

                Cell newCell = new Cell(newStep, newRow, newCol, newK, Math.abs(newRow - m + 1) + Math.abs(newCol - n + 1));
                q.offer(newCell);
                
            }
            
        }
        return -1; 
    }
}
```



##### Complexity:



- Time: O(m*n*k)
because we are iterating every cell when there are k steps remaining at most once.
- Space(m*n*k) 
same here, we are storing cells at most m * n * k in our priority queue 
## **Reference**