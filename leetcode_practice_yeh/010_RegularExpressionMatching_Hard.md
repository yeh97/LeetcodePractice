

### Leetcode 10
#### [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching)
  
_Implement regular expression matching with support for '.' and '*'._

    '.' Matches any single character.
    '*' Matches zero or more of the preceding element.
    
    The matching should cover the entire input string (not partial).
    
    The function prototype should be:
bool isMatch(const char *s, const char *p)

**examples:**
> * isMatch("aa","a") ? false
> * isMatch("aa","aa") ? true
> * isMatch("aaa","aa") ? false
> * isMatch("aa", "a*") ? true
> * isMatch("aa", ".*") ? true
> * isMatch("ab", ".*") ? true
> * isMatch("aab", "c*a*b") ? true

  

``` java
/*
 *Author: yeh
 *Time: 2017_07_08
 *Language: Java
 *
 */
public class Solution {
    public boolean isMatch(String s, String p) {
        if(s==null || p==null) return s==null && p==null;
        return isMatch(s.toCharArray(), 0, p.toCharArray(), 0);
    }
    private static boolean isMatch(char[] s, int is, char[] p, int ip) {
        //assert(s!=null && p!=null)
        if(ip>=p.length) return is>=s.length;
        //next char is '*', p[ip] may appear 0/1/2/... times
        if(ip<p.length-1 && p[ip+1]=='*') {
            while(is<s.length && (p[ip]==s[is] || p[ip]=='.')) {
                //think p[ip] appear is(now) - is(input) times
                if(isMatch(s, is, p, ip+2)) return true;
                is++;
            }
            return isMatch(s, is, p, ip+2);
        }else{
            return (is<s.length) && (p[ip]==s[is] || p[ip]=='.') 
                ? isMatch(s, is+1, p, ip+1) : false;
        }
    }
}

```

