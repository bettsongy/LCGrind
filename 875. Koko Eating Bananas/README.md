
###### tags:
Array, Binary Search
###### date: 

[leetcode link](https://leetcode.com/problems/koko-eating-bananas/)

## **Description**

Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer k such that she can eat all the bananas within h hours.
A car fleet is some non-empty set of cars driving at the same position and same speed. Note that a single car is also a car fleet.

If a car catches up to a car fleet right at the destination point, it will still be considered as one car fleet.

Return the number of car fleets that will arrive at the destination.

#### Example 1

Input: piles = [3,6,7,11], h = 8
Output: 4
#### Example 2

Input: piles = [30,11,23,4,20], h = 5
Output: 30

#### Constraints

1 <= piles.length <= 104
piles.length <= h <= 109
1 <= piles[i] <= 109

## **Solution**

### Approach 1: 

##### Code:

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int left = 1;
        int right = 1000000000;
        
        while(left < right){
            int mid = left + (right - left) / 2; 
            if(getEatingTime(piles, mid) <= h){
                right = mid; 
            }else{
                left = mid + 1; 
                
            }
            
        }
        return left; 
        
        
    }
    
    private int getEatingTime(int[] piles, int speed){
        
        int time = 0;
        for(int i = 0; i < piles.length; i ++){
            time += piles[i] / speed;
            if(piles[i] % speed > 0){
                time ++; 
            }
        }
        return time; 
        
        
    }
    
    
}
```

##### Complexity:
- Time: O(NlogK) the binary search is logK where K is the range of our eating time, iterate though all the item N linearily takes O(n) in the function
- Space: O(1) we are not using any additional data structure

## **Reference**