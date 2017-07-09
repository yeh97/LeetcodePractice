

### Leetcode 6
###### [ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion)
  
*The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)*

    P   A   H   N
    A P L S I I G
    Y   I   R
  
*And then read line by line: `"PAHNAPLSIIGYIR"`*

    Write the code that will take a string and make this conversion given a number of rows:
    
    string convert(string text, int nRows);
  
*`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.*
  

``` java
/*
 *Author: yeh
 *Time: 2017_07_07
 *Language: Java
 *
 */
public class Solution {
    public String convert(String s, int numRows) {
        if(s == null) return null;
        if(s.length()==0 || numRows<2) return s;
        char[] ret = new char[s.length()];
        int cnt = 0;
        //a cycle's length
        int mod = (numRows-1)<<1;
        int t;
        for(int i=0; i<numRows; i++) {
            for(int j=i; j<ret.length; j+=mod) {
                ret[cnt++] = s.charAt(j);
                //not in first or last row, should add two char
                if(i>0 && i<numRows-1 && (t=j+mod-2*i)<ret.length) {
                    ret[cnt++] = s.charAt(t);
                }
            }
        }
        return new String(ret);
    }
}

```



