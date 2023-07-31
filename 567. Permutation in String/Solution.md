###### tags:

HashTable, Sliding Window
 
###### date: 

7/30/2023

[leetcode link](https://leetcode.com/problems/permutation-in-string/)

## **Description**

Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

 


#### Example 1

Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
Example 2:

Input: s1 = "ab", s2 = "eidboaoo"
Output: false

#### Constraints

1 <= s1.length, s2.length <= 104
s1 and s2 consist of lowercase English letters.

## **Solution**



### Approach 1: 

##### Code:

```java
class Solution {

    public boolean checkInclusion(String s1, String s2) {
        int valid = 0;

        HashMap<Character, Integer> s1Map = new HashMap<>();
        HashMap<Character, Integer> window = new HashMap<>();
        for (char ch : s1.toCharArray()) {
            s1Map.put(ch, s1Map.getOrDefault(ch, 0) + 1);
        }

        int left = 0;

        for (int right = 0; right < s2.length(); right++) {
            char rightCh = s2.charAt(right);
            if (s1Map.containsKey(rightCh)) {
                window.put(rightCh, window.getOrDefault(rightCh, 0) + 1);
                if (window.get(rightCh).equals(s1Map.get(rightCh))) {
                    valid++;
                }
            }

            while (valid >= s1Map.size()) {
                if (right - left + 1 == s1.length()) {
                    return true;
                }

                char leftCh = s2.charAt(left);
                left++;

                if (window.containsKey(leftCh)) {
                    if (window.get(leftCh).equals(s1Map.get(leftCh))) {
                        valid--;
                    }
                    window.put(leftCh, window.get(leftCh) - 1);
                }
            }
        }

        return false;
    }
}

```

##### Complexity:
- Time: O(n) because we are iterating every character at most twice. Right pointer and left pointer each once')'
- Space: O(1) we only creating a HashTable, and at most its the size of the key is 26, so it is not growing proportion to the size of the input string

## **Reference**