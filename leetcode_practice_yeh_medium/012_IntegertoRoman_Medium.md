

### Leetcode 12
#### [Integer to Roman](https://leetcode.com/problems/integer-to-roman)

    Given an integer, convert it to a roman numeral.
    
    Input is guaranteed to be within the range from 1 to 3999.
    

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_09
 *Language: Java
 *
 */

public class Solution {
    //M 1000 D 500 C 100 L 50 X 10 V 5 I 1
    public static final String RomanIndex[] = {
        "","I","II","III","IV","V","VI","VII","VIII","IX",
        "","X","XX","XXX","XL","L","LX","LXX","LXXX","XC",
        "","C","CC","CCC","CD","D","DC","DCC","DCCC","CM",
        "","M","MM","MMM","","","","","",""
    };
    public String intToRoman(int num) {
        return (num<=0 || num>3999) ? 
            "" : (RomanIndex[30+num/1000] + RomanIndex[20+num/100%10] + 
                  RomanIndex[10+num/10%10] + RomanIndex[num%10]);
    }
}

```
