


### Leetcode 204
#### [Count Primes](https://leetcode.com/problems/count-primes)

  

##### ***Problem:***

	Count the number of prime numbers (<n).
	
##### ***Example:***

    Input: 3
        Output: 1

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_09
 *Language: Java
 *
 */

class Solution {
    public int countPrimes(int n) {
        // 2018/2/9 : 12ms
        // Sieve of Eratosthenes
        if (n <= 2) return 0;
        int res = n / 2;
        boolean[] isnotPrime = new boolean[n];
        for (int i = 3; i * i < n; i += 2) {
            if (isnotPrime[i]) continue;
            for (int j = i * i; j < n; j += i * 2) {
                if (isnotPrime[j]) continue;
                isnotPrime[j] = true;
                res--;
            }
        }
        return res;
    }
}

```
