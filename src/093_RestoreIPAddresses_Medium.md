

### Leetcode 93
#### [Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses)

  

##### ***Problem:***

    Given a string containing only digits, 
    restore it by returning all possible valid IP address combinations.
    

##### ***Example:***

    Input: "25525511135"
        Output: ["255.255.11.135", "255.255.111.35"]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_10
 *Language: Java
 *
 */

public class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> ret = new ArrayList<String>();
        if (s == null) return ret;
        // "0.0.0.0" ~ "255.255.255.255"
        if (s.length() < 4 || s.length() > 12) return ret;
        restoreIpAddressesDFS(s, "", ret, 0);
        return ret;
    }
    private void restoreIpAddressesDFS(String str, String solution, 
                                       List<String> list, int dotNum) {
        if (dotNum == 3) {
            if (validNum(str)) list.add(solution + str);
        } else {
            // every part : * ... ***
            int end = Math.min(3, str.length() - 1);
            // a part of str
            String substr = null;
            for (int i = 0; i < end; i++) {
                substr = str.substring(0, i + 1);
                if (!validNum(substr)) continue;
                restoreIpAddressesDFS(str.substring(i + 1, str.length()), 
                                      solution + substr + '.', list, dotNum + 1);
            }
        }
    }
    private boolean validNum(String s) {
        if (s == null || s.length() == 0) return false;
        // s : 0
        if (s.charAt(0) == '0') return s.length() == 1;
        // s : 1...255
        int num = Integer.parseInt(s);
        return num > 0 && num < 256;
    }
}

```


