###### tags:

String

###### date: 

7/30/2023

[leetcode link](https://leetcode.com/problems/zigzag-conversion/)

## **Description**

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows);

#### Example 1

Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"

#### Example 2

Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I

#### Example 3
Input: s = "A", numRows = 1
Output: "A"



#### Constraints

1 <= s.length <= 1000
s consists of English letters (lower-case and upper-case), ',' and '.'.
1 <= numRows <= 1000

## **Solution**




### Approach 1: 

##### Code:

```java

class Solution {
    public String convert(String s, int numRows) {
        
        if(numRows == 1){
            return s; 
        }
        
        // Math.min() is to handle the case where the number of character 
        // in the String s is less than the number of rows
        StringBuilder[] sbRows = new StringBuilder[Math.min(numRows, s.length())];
        
        for(int i = 0; i < sbRows.length; i ++){
            sbRows[i] = new StringBuilder();
        }
        
        int currRow = 0; 
        boolean goingDown = false; 
        
        for(int i = 0; i < s.length(); i ++){
            
            if(currRow == 0  || currRow == numRows - 1){
                goingDown = !goingDown; 
            }
            
            sbRows[currRow].append(s.charAt(i));
            
            if(goingDown){
                currRow ++;     
            }else{
                currRow --;
            }
        }
        
        StringBuilder res = new StringBuilder();
        for(StringBuilder sb : sbRows){
            res.append(sb.toString());
        }
        return res.toString(); 
        
    }
}

```

##### Complexity:
- Time: O(n) because we are iterating every character in the string s only once
- Space: O(n) we create additional stringbuilder to store those character in the string s 

## **Reference**