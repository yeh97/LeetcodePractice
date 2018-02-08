

### Leetcode 22
#### [Generate Parentheses](https://leetcode.com/problems/generate-parentheses)

    Given n pairs of parentheses, 
    write a function to 
    generate all combinations of well-formed parentheses.
 
 ***Example:***
 
    Input: -1
        Ouput: []
    Input: 0
        Ouput: [""]
    Input: 2
        Ouput: ["(())", "()()"]

``` java
/*
 *Author: yeh
 *Time: 2017_07_11
 *Language: Java
 *
 */

public class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ret = new LinkedList<String>();
        if(n < 0) return ret;
        String str = "";
        generateParenthesisHelper(ret, str, n, n);
        return ret;
    }
    //dfs
    private static void generateParenthesisHelper(
        List<String> list, String str, int left, int right) {
        //right : the number of unusing ')', left : unusing '('
        if(right < left) return;
        if(left > 0) generateParenthesisHelper(list, str+"(", left-1, right);
        if(right > left) generateParenthesisHelper(list, str+")", left, right-1);
        if(right == 0) list.add(str);
    }
}

```
