
###### tags:
Stack, String, Recursion
###### date: 

[leetcode link](https://leetcode.com/problems/basic-calculator-iii/)

## **Description**

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only non-negative integers, '+', '-', '*', '/' operators, and open '(' and closing parentheses ')'. The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of [-231, 231 - 1].

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval().

#### Example 1

Input: s = "1+1"
Output: 2

#### Example 2

Input: s = "6-4/2"
Output: 4

#### Constraints

1 <= s <= 104
s consists of digits, '+', '-', '*', '/', '(', and ')'.
s is a valid expression.

## **Solution**

### Approach 1: 

##### Code:

```java
class Solution {
    public int calculate(String s) {
        return compute(s);
    }
    
    int index = 0; 
    public int compute(String s){
        
        Stack<Integer> stack = new Stack<>(); 
        int num = 0; 
        char op = '+';

        while(index < s.length()){
            
            char ch = s.charAt(index++);
            if(Character.isDigit(ch)){
                num = num * 10 + (ch - '0'); 
            }
            
            if(ch == '('){
                num = compute(s);
            }
            
            if(!Character.isDigit(ch) || index == s.length()){
                if(op == '+'){
                    stack.push(num);
                }else if(op == '-'){
                    stack.push(-num);
                }else if(op == '/'){
                    stack.push(stack.pop() / num);
                }else if(op == '*'){
                    stack.push(stack.pop() * num);
                }
                
                num = 0;
                op = ch; 
            }
            
            
            
            if(ch == ')'){
                break; 
            }
        }
        int sum = 0;
        while(!stack.isEmpty()){
            sum += stack.pop();
        }
        
        return sum; 
        
    }
}
```

##### Complexity:
- Time: O(n) the while loop iterates n so its O(n)
- Space: O(n) the stack will be storing at most n. 

## **Reference**