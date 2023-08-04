###### tags:

Array, Binary Search

###### date: 

08/04/2023

[leetcode link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)



## **Description**

Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.


#### Example 1

Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.
#### Example 2

Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

#### Constraints


1 <= s.length, p.length <= 3 * 104
s and p consist of lowercase English letters.

## **Solution**



### Approach 1: 

##### Code:

```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        while(left < right){
            int mid = left + (right - left) / 2; 
            if(nums[mid] > nums[right]){
                left = mid + 1; 
            }else{
                right = mid; 
            }
        }
        return nums[left]; 
    }
}
```

##### Complexity:
- Time: O(logN) because we are iterating the range in binary search, so its log
- Space: O(1) we are not creating any new data structure so its constant

## **Reference**