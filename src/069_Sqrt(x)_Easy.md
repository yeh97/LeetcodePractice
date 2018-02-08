

### Leetcode 69
#### [Sqrt(x)](https://leetcode.com/problems/sqrtx)

##### ***Problem:***

    Implement int sqrt(int x).

    Compute and return the square root of x.


##### ***Example:***
 
    Input: 0
        Ouput: 0
    

##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_06
 *Language: Java
 *
 */

public class Solution {
    public int mySqrt(int x) {
        if (x < 0) return Integer.MIN_VALUE;
        if (x == 0) return 0;
        int l = 1;
        int r = x / 2 + 1;
        int m = l + (r - l) / 2;
        int prem = 0;
        while (prem != m) {
            if (m > x / m) r = m;
            else l = m;
            prem = m;
            m = l + (r - l) / 2;
        }
        return m;
    }
}

```

##### *Method: #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_06
 *Language: Java
 *
 */

public class Solution {
    public int mySqrt(int x) {
        if (x < 0) return Integer.MIN_VALUE;
        if (x == 0) return 0;
        //NewTon
        int m = x;
        while (m > x / m) {
            //m = (m + x / m) / 2;
            m = x / m + (m - x / m) / 2;
        }
        return m;
    }
}

```

##### *Method: #3*
``` java
/*
 *Author: yeh
 *Time: 2017_08_06
 *Language: Java
 *
 */

public class Solution {
    public int mySqrt(int x) {
        if (x < 0) return Integer.MIN_VALUE;
        if (x == 0) return 0;
        int val = (int) (mySqrt((double) x));
        return val * val > x ? val - 1 : val;
    }
    public double mySqrt(double x) {
        double xhalf = 0.5 * x;
        long i = Double.doubleToRawLongBits(x);
        i = 0x5fe6ec85e7de30daL - (i >> 1);
        x = Double.longBitsToDouble(i);
        //newton 2 times
        x = x * (1.5 - xhalf * x * x);
        x = x * (1.5 - xhalf * x * x);
        return 1 / x;
    }
}


```

