

### Leetcode 49
#### [Group Anagrams](https://leetcode.com/problems/group-anagrams)

  

##### ***Problem:***

    Given an array of strings, group anagrams together.
    
##### ***Note:***

    All inputs will be in lower-case.
    
##### ***Example:***

    Input: ["eat", "tea", "tan", "ate", "nat", "bat"]
        Output: [["ate", "eat","tea"], ["nat","tan"], ["bat"]]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_31
 *Language: Java
 *
 */

public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> ret = new ArrayList<List<String>>();
        if (strs == null || strs.length == 0) {
            return ret;
        }
        Map<String, Integer> map = new HashMap<String, Integer>();
        for (String str : strs) {
            char[] chs = str.toCharArray();
            Arrays.sort(chs);
            String t = new String(chs);
            if (map.containsKey(t)) {
                ret.get(map.get(t)).add(str);
            } else {
                List<String> newlist = new LinkedList<String>();
                map.put(t, ret.size());
                ret.add(newlist);
                newlist.add(str);
            }
        }
        return ret;
    }
}

```

