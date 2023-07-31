###### tags:

Array, HashTable, Counting

###### date: 

7/30/2023

[leetcode link](https://leetcode.com/problems/find-all-anagrams-in-a-string/)



## **Description**

Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.


#### Example 1


Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
Example 2:
#### Example 2

Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
 

#### Constraints


1 <= s.length, p.length <= 3 * 104
s and p consist of lowercase English letters.

## **Solution**



### Approach 1: 

##### Code:

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        
        HashMap<Character, Integer> map = new HashMap<>();
        HashMap<Character, Integer> window = new HashMap<>();

        for(Character ch : p.toCharArray()){
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }
        int valid = 0; 
        List<Integer> list = new LinkedList<>();
        int left = 0; 
        for(int right = 0; right < s.length(); right ++){
            
            char rightCh = s.charAt(right);
            if(map.containsKey(rightCh)){
                window.put(rightCh, window.getOrDefault(rightCh, 0) + 1);
                if(map.get(rightCh).equals(window.get(rightCh))){
                    valid ++; 
                }
                
            }
                   
            while(valid == map.size()){
                
                if(right - left + 1 == p.length()){
                    list.add(left);
                }
                char leftCh = s.charAt(left);
                left ++;
                if(map.containsKey(leftCh)){
                    if(map.get(leftCh).equals(window.get(leftCh))){
                        valid --;
                    }
                    window.put(leftCh, window.get(leftCh) - 1);
                    
                }
                
                
            }
                   
        }
        return list;           
        
        
    }
}
```

##### Complexity:
- Time: O(n) because we are iterating the string at most two times one with left and right pointers
- Space: O(1) we only creating a hashmap with 26 keys at most, so its constant 

## **Reference**