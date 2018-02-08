

### Leetcode 32
#### [Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses)

  

##### ***Problem:***

    Given a string containing just the characters '(' and ')',
    
    find the length of the longest valid 
    (well-formed) parentheses substring.
    
##### ***Example:***

    Input: "(()"
        Output: 2 ("()")
    Input: ")()())"
        Ouput: 4 ("()()")

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_16
 *Language: Java
 *
 */

public class Solution {
    public int longestValidParentheses(String s) {
        if(s==null || s.length()==0) return 0;
        int ret = 0;
        int length = s.length();
        Stack<Integer> t = new Stack<Integer>();
        //the spild window
        int l = 0;
        for(int r=0; r<length; r++) {
            if(s.charAt(r) == '(') {
                t.push(r);
            }else if(s.charAt(r) == ')') {
                if(t.empty()) {
                    //match error if l is the left of window
                    l = r + 1;
                }else{
                    t.pop();
                    if(t.empty()) {
                        //the Parentheses: s[l]...s[r]
                        ret = Math.max(ret, r-l+1);
                    }else{
                        //Example: ((()
                        ret = Math.max(ret, r-t.peek());
                    }
                }
            }
        }
        return ret;
    }
}

```

##### *Method #2*

``` java
/*
 *Author: yeh
 *Time: 2017_07_16
 *Language: Java
 *
 */

public class Solution {
    public int longestValidParentheses(String s) {
        if(s==null || s.length()==0) return 0;
        int ret = 0;
        int length = s.length();
        //the num of '(' in possible Valid Parentheses
        int lnum = 0;
        //the num of ')'
        int rnum = 0;
        //the left of Longest Valid Parentheses == '(' 
        //&& the right == ')' is impossible
        //So sacnning from two direction is ok
        //scanning from left to right
        for(int i=0; i<length; i++) {
            if(s.charAt(i) == '(') {
                lnum++;
            }else{
                rnum++;
            }
            if(lnum == rnum) {
                ret = Math.max(ret, lnum<<1);
            }else if(rnum > lnum) {
                lnum = rnum = 0;
            }
        }
        lnum = rnum = 0;
        //scanning from right to left
        for(int i=length-1; i>=0; i--) {
            if(s.charAt(i) == '(') {
                lnum++;
            }else{
                rnum++;
            }
            if(lnum == rnum) {
                ret = Math.max(ret, lnum<<1);
            }else if(lnum > rnum) {
                lnum = rnum = 0;
            }
        }
        return ret;
    }
}

```

