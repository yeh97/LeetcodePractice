

### Leetcode 28
#### [Implement strStr()](https://leetcode.com/problems/implement-strstr)

##### ***Problem:***

    Returns the index of the first occurrence of needle in haystack, 
    or -1 if needle is not part of haystack.


##### ***Example:***
 
    Input: "abcc", "bc"
    Ouput: 1
    

  
##### *Method: #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_14
 *Language: Java
 *
 */

public class Solution {
    public int strStr(String haystack, String needle) {
        if(haystack==null || needle==null) return -1;
        if(needle.length() == 0) return 0;
        int hlen = haystack.length();
        int nlen = needle.length();
        //Brute Force
        for(int i=0; i<=hlen-nlen; i++) {
            if(needle.equals(haystack.substring(i, i+nlen))) {
                return i;
            }
        }
        return -1;
    }
}


```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_07_14
 *Language: Java
 *
 */

public class Solution {
    public int strStr(String haystack, String needle) {
        int[] next = getNextArrayOfKMP(needle);
        int nlen = needle.length();
        int hlen = haystack.length();
        int nindex = 0;
        int hindex = 0;
        //Match
        while(nindex<nlen && hindex<hlen) {
            if(nindex==-1 || haystack.charAt(hindex)==needle.charAt(nindex)) {
                nindex++;
                hindex++;
            }else{
                nindex = next[nindex];
            }
        }
        return (nindex==nlen) ? hindex-nlen : -1;
    }
    public static int[] getNextArrayOfKMP(String str) {
        if(str==null || str.length()==0) return null;
        int length = str.length();
        //Next Array: next[i] mean : the longest length
        //of elements in prefixion && suffix of str[0,...,i-1]
        int[] next = new int[length+1];
        next[0] = -1;
        int index = 0;
        int j = -1;
        while(index < length-1) {
            if(j==-1 || str.charAt(index)==str.charAt(j)) {
                index++;
                j++;
                next[index] = str.charAt(index)==str.charAt(j) ? next[j] : j;
            }else{
                j = next[j];
            }
        }
        return next;
    }
}
```

