

### Leetcode 13
#### [Roman to Integer](https://leetcode.com/problems/roman-to-integer)

    Given a roman numeral, convert it to an integer.
    
    Input is guaranteed to be within the range from 1 to 3999.
    

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_09
 *Language: Java
 *
 */

public class Solution {
    public int romanToInt(String s) {
        int ret = 0;
        int size = s==null ? 0:s.length();
        if(size == 0) return ret;
        int[] sigalRoman = new int[size];
        for(int i=0; i<size; i++) {
            sigalRoman[i] = sigalRomanToInt(s.charAt(i));
        }
        
        for(int i=0; i<size; i++) {
            //the transform's rule
            if(i>0 && sigalRoman[i]>sigalRoman[i-1]) {
                ret += sigalRoman[i] - 2*sigalRoman[i-1];
            }else{
                ret += sigalRoman[i];
            }
        }
        return ret;
    }
    public static int sigalRomanToInt(char c) {
        switch (c) {
            case 'I' : return 1;
            case 'V' : return 5;
            case 'X' : return 10;
            case 'L' : return 50;
            case 'C' : return 100;
            case 'D' : return 500;
            case 'M' : return 1000;
            default : return 0;
        }
    }
}

```
