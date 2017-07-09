

### Leetcode 9
#### [Palindrome Number](https://leetcode.com/problems/palindrome-number)
  
    Determine whether an integer is a palindrome.
    Do this without extra space.

**Hint:**

    Could negative integers be palindromes? (ie, -1)
    note the restriction of using extra space.
    the reversed integer might overflow.

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_08
 *Language: Java
 *
 */
public class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0) return false;
        if(x == 0) return true;
        return reverse(x)==x;
    }
    //leetcode_7: Reverse Integer
    public static int reverse(int x) {
        // -Integer.MIN_VALUE == Integer.MIN_VALUE
        if(x == Integer.MIN_VALUE) return 0;
        if(x < 0) return -reverse(-x);
        long t = x;
        long ans = 0;
        while(t!=0){
            ans = ans*10 + t%10;
            t /= 10;
        }
        return (ans > Integer.MAX_VALUE) ? 0 : (int)ans;
    }
}
```


