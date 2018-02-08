

### Leetcode 150
#### [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation)

  

##### ***Problem:***

    Evaluate the value of an arithmetic expression in Reverse Polish Notation.

	Valid operators are +, -, *, /. 
	
	Each operand may be an integer or another expression.
    
##### ***Example:***

    Input: ["4", "13", "5", "/", "+"]
        Output: 6


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_28
 *Language: Java
 *
 */

class Solution {
    public int evalRPN(String[] tokens) {
	    // 2018/1/28 : 12ms
        if (tokens == null || tokens.length == 0) return 0;
        Stack<Integer> t = new Stack<Integer>();
        for (int i = 0; i < tokens.length; i++) {
            switch (tokens[i]) {
                case "+":
                    t.push(t.pop() + t.pop()); break;
                case "-":
                    t.push(-t.pop() + t.pop()); break;
                case "*":
                    t.push(t.pop() * t.pop()); break;
                case "/":
                    int a = t.pop();
                    int b = t.pop();
                    t.push(b / a); break;
                default:
                    t.push(Integer.valueOf(tokens[i]));
            }
        }
        int res = t.pop();
        return t.empty() ? res : 0;
    }
}

```

