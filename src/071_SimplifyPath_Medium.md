

### Leetcode 71
#### [Simplify Path](https://leetcode.com/problems/simplify-path)

  

##### ***Problem:***

    Given an absolute path for a file (Unix-style), simplify it.
    
##### ***Note:***

    1) double ended queue or stack
    
##### ***Example:***

    Input: "/a/./b/../../c/"
        Output: "/c"


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_07
 *Language: Java
 *
 */

public class Solution {
    public String simplifyPath(String path) {
        if (path == null) return null;
        Deque<String> dq = new ArrayDeque<String>();
        int length = path.length();
        String name = null;
        //dq <--> stack
        for (int i = 0; i < length; i++) {
            //ignore '/'
            while (i < length && path.charAt(i) == '/') {
                i++;
            }
            //record name of path between two '/'
            name = "";
            while (i < length && path.charAt(i) != '/') {
                name += path.charAt(i++);
            }
            //".." back to last catalog
            //empty or "." has no meaning
            if ("..".equals(name)) {
                if (!dq.isEmpty()) dq.pollLast();
            } else if (!name.isEmpty() && !".".equals(name)) {
                dq.offerLast(name);
            }
        }
        if (dq.isEmpty()) return "/";
        StringBuilder ret = new StringBuilder();
        //dq <--> queue
        while (!dq.isEmpty()) {
            ret.append("/");
            ret.append(dq.pollFirst());
        }
        return ret.toString();
    }
}
```

