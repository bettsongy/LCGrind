###### tags:

Array, HashTable, Counting

###### date: 

7/30/2023

[leetcode link](https://leetcode.com/problems/minimum-window-substring/)



## **Description**

Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

#### Example 1

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

#### Example 2

Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
Example 3:

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
 

#### Constraints

Constraints:

m == s.length
n == t.length
1 <= m, n <= 105
s and t consist of uppercase and lowercase English letters.

## **Solution**



### Approach 1: 

##### Code:

```java
class Solution {
    public String minWindow(String s, String t) {
        HashMap<Character, Integer> window = new HashMap<>();
        HashMap<Character, Integer> map = new HashMap<>();
        for(Character ch : t.toCharArray()){
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }
        
        int minLeft = 0;
        int minRight = 0; 
        int minWindow = Integer.MAX_VALUE;
        int left = 0;
        int valid = 0; 
        for(int right = 0; right < s.length(); right ++){
            
            char rightCh = s.charAt(right);
            if(map.containsKey(rightCh)){
                
                window.put(rightCh, window.getOrDefault(rightCh, 0) + 1);
                if(window.get(rightCh).equals(map.get(rightCh))){
                    valid ++; 
                }
                
            }
            
            while(valid >= map.size()){
                if(right - left + 1 < minWindow){
                    minWindow = right - left + 1; 
                    minLeft = left;
                    minRight = right; 
                }
                 char leftCh = s.charAt(left);
                 left ++; 
                 if(map.containsKey(leftCh)){
                     
                     if(map.get(leftCh).equals(window.get(leftCh)))                      {
                        valid --;     
                     }
                     window.put(leftCh, window.get(leftCh) - 1);
                     
                 }
                
            }   
        }
        if(minWindow == Integer.MAX_VALUE){
            return "";
        }
        return s.substring(minLeft, minRight + 1);
        
    }
}
```

##### Complexity:
- Time: O(n) because we are iterating the string at most two times one with left and right pointers
- Space: O(1) we only creating a hashmap with 26 keys at most, so its constant 

## **Reference**