


### Leetcode 202
#### [Happy Number](https://leetcode.com/problems/happy-number)

  

##### ***Problem:***

	A happy number is a number defined by the following process: 
	Starting with any positive integer, 
	replace the number by the sum of the squares of its digits, 
	and repeat the process until the number equals 1 (where it will stay), 
	or it loops endlessly in a cycle which does not include 1. 

	Those numbers for which this process ends in 1 are happy numbers.
	Write an algorithm to determine if a number is "happy".
	
##### ***Example:***

    Input: 19
        Output: true (19->82->68->100->1)

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_09
 *Language: Java
 *
 */

class Solution {
    public boolean isHappy(int n) {
        // 2018/2/9 : 2ms
        if (n <= 0) return false;
        // n1 -> n2 -> ..., as a linkedlist
        // return elem in circle is 1
        int slow = n, fast = n;
        do {
            slow = next(slow);
            fast = next(next(fast));
        } while (slow != fast);
        return slow == 1;
    }
    private int next(int n) {
        int res = 0;
        for(int i = n; i > 0; i /= 10) res += square(i % 10);
        return res;
    }
    private int square(int n) { return n * n; }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_02_09
 *Language: Java
 *
 */

class Solution {
    public boolean isHappy(int n) {
        // 2018/2/9 : 1ms
        if (n <= 0) return false;
        // unHappy numbers, must appear 4
        while (n != 1 && n != 4) {
            n = next(n);
        }
        return n == 1;
    }
    private int next(int n) {
        int res = 0;
        for(int i = n; i > 0; i /= 10) res += square(i % 10);
        return res;
    }
    private int square(int n) { return n * n; }
}


```

