###### tags:

String, Stack
 
###### date: 

7/30/2023

[leetcode link](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/)

## **Description**

You are given a string s that consists of lower case English letters and brackets.

Reverse the strings in each pair of matching parentheses, starting from the innermost one.

Your result should not contain any brackets.

#### Example 1

Input: s = "(abcd)"
Output: "dcba"

#### Example 2

Input: s = "(u(love)i)"
Output: "iloveu"
Explanation: The substring "love" is reversed first, then the whole string is reversed.


#### Example 3

Input: s = "(ed(et(oc))el)"
Output: "leetcode"
Explanation: First, we reverse the substring "oc", then "etco", and finally, the whole string.

#### Constraints

1 <= s.length <= 2000
s only contains lower case English characters and parentheses.
It is guaranteed that all parentheses are balanced

## **Solution**



### Approach 1: 

##### Code:

```java
class Solution {
    public String reverseParentheses(String s) {
        Deque<Character> stack = new LinkedList<>(); 
        for(char ch : s.toCharArray()){
            
            if(ch == ')'){
                
                StringBuilder sb = new StringBuilder(); 
                while(!stack.isEmpty() && stack.peek() != '('){
                    
                    sb.append(stack.poll());
                    
                }
                if(!stack.isEmpty()){
                    stack.poll();
                }
                
                for(char c : sb.toString().toCharArray()){
                    stack.push(c);
                }    
            }else{
                stack.push(ch);
            }
            
            
        }
        StringBuilder res = new StringBuilder();
        while(!stack.isEmpty()){
            res.append(stack.poll());
        }
        return res.reverse().toString();
        
    }
}
```

##### Complexity:
- Time: O(n) because we are iterating every character at most twice. Once when we first push it, another time when we reverse it when we encounter the character ')'
- Space: O(n) we only creating a stack, and at most its the size of n 

## **Reference**