

### Leetcode 20
#### [Valid Parentheses](https://leetcode.com/problems/valid-parentheses)

    Given a string containing just the characters 
    '(', ')', '{', '}', '[' and ']',
    determine if the input string is valid.
 
 ***Example:***
 
    The brackets must close in the correct order, 
    "()" and "()[]{}" are all valid 
    but "(]" and "([)]" are not.
    

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_11
 *Language: Java
 *
 */

public class Solution {
    public boolean isValid(String s) {
        if(s==null || s.length()==0) return true;
        if(s.length()%2 == 1) return false;
        Stack<Character> st = new Stack<Character>();
        char[] sarray = s.toCharArray();
        for(char ch : sarray) {
            if(ch == '(') {
                st.push(')');
            }else if(ch == '[') {
                st.push(']');
            }else if(ch == '{') {
                st.push('}');
            }else{//ch is right of bracket
                if(st.empty() || st.peek()!=ch) return false;
                st.pop();
            }
        }
        return st.empty();
    }
}

```
