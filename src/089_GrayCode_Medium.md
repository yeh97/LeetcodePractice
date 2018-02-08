

### Leetcode 89
#### [Gray Code](https://leetcode.com/problems/gray-code)

  

##### ***Problem:***

    The gray code is a binary numeral system 
    where two successive values differ in only one bit.

    Given a non-negative integer n representing the total number of bits in the code, 
    print the sequence of gray code. 
    A gray code sequence must begin with 0.

##### ***Example:***

    Input: 2
        Output: [0,1,3,2] (00->01->11->10)

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_09
 *Language: Java
 *
 */

public class Solution {
    public List<Integer> grayCode(int n) {
        // a solution of grayCode(n) :
        // <'0' + grayCode(n - 1)>
        // + <'1' + reverse(grayCode(n - 1))
        List<Integer> ret = new ArrayList<Integer>();
        ret.add(0);
        int addInLeft = 1;
        for (int i = 0; i < n; i++) {
            for (int j = ret.size() - 1; j >= 0; j--) {
                ret.add(ret.get(j) + addInLeft);
            }
            addInLeft <<= 1;
        }
        return ret;
    }
}
```


