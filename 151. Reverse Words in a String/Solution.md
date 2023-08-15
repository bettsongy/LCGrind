###### tags:

Array, HashMap

###### date:

08/05/2023

[leetcode link](https://leetcode.com/problems/reverse-words-in-a-string/)

## **Description**

Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

#### Example 1

Input: s = "the sky is blue"
Output: "blue is sky the"

#### Example 2

Input: s = " hello world "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.

#### Constraints

1 <= nums.length <= 105
-109 <= nums[i] <= 109
0 <= k <= 105

## **Solution**

### Approach 1:

##### Code:

```java
class Solution {
    public String reverseWords(String s) {
        String[] words = s.split("\\s+");
        for(int i = 0; i < words.length / 2; i ++){
            String temp = words[words.length - i - 1];
            words[words.length - i - 1] = words[i];
            words[i] = temp;

        }
        StringBuilder sb = new StringBuilder();
        for(String word : words){
            sb.append(word);
            sb.append(" ");
        }
        sb.setLength(sb.length() - 1);
        return sb.toString().trim();
    }
}
```

##### Complexity:

- Time: O(N) because we are iterating the size of the string in linear time
- Space: O(N) we are storing the string

## Follow-up: If the string data type is mutable in your language, can you solve it in-place with O(1) extra space?

```JAVA
class Solution {
    public String reverseWords(String s) {

        char[] sArr  = s.toCharArray();
        reverse(sArr, 0, s.length() - 1);

        int start = 0;
        for(int i = 0; i < s.length(); i ++){

            if(sArr[i] == ' '){
                reverse(sArr, start, i - 1);
                start = i + 1;
            }

        }

        if(start < s.length()){
            reverse(sArr, start, sArr.length - 1);
        }

        StringBuilder sb = new StringBuilder();
        boolean prevSpace = false;
        for(char ch : sArr){
            if(ch != ' ' || !prevSpace){
                sb.append(ch);
            }
            prevSpace = ch == ' ';

        }
        return sb.toString().trim();

    }

    private void reverse(char[] s, int left, int right){


        while(left < right){

            char temp = s[right];
            s[right] = s[left];
            s[left] = temp;
            left ++;
            right --;

        }
    }
}

```

## **Reference**
