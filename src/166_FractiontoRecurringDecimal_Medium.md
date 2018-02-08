


### Leetcode 166
#### [Fraction to Recurring Decimal](https://leetcode.com/problems/fraction-to-recurring-decimal)

  

##### ***Problem:***

    Given two integers representing the numerator and denominator of a fraction, 
    return the fraction in string format.

	If the fractional part is repeating, 
	enclose the repeating part in parentheses.
    
##### ***Example:***

    Input: 1,6
        Output: 0.1(6)


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_03
 *Language: Java
 *
 */

class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        // 2018/2/3 : 2ms
        // N = (denominator / gcd(denominator, numerator))
        // O(N) or O(NlgN)
        if (denominator == 0) return ""; // err
        if (numerator == 0) return "0";
        StringBuilder res = new StringBuilder((numerator > 0 ^ denominator > 0) ? "-" : "");
        // abs(Integer.MIN_VALUE) > Integer.MAX_VALUE
        long n = Math.abs((long) numerator);
        long d = Math.abs((long) denominator);
        res.append(n / d);
        if (n % d == 0) return res.toString();
        res.append(".");
        // remainder -> index -> start of repetend
        HashMap<Integer, Integer> rmap = new HashMap<Integer, Integer>();
        long r = n % d;
        int index = res.length();
        for (r *= 10; r != 0 && !rmap.containsKey((int) r); r = r % d * 10) {
            rmap.put((int) r, index++);
            res.append(r / d);
        }
        return r == 0 ? res.toString() : res.insert((int) rmap.get((int) r), '(').append(')').toString();
    }
}


```


