

### Leetcode 140
#### [Word Break II](https://leetcode.com/problems/word-break-ii)

  

##### ***Problem:***

    Given a non-empty string s and 
    a dictionary wordDict containing a list of non-empty words, 
    add spaces in s to construct a sentence 
    where each word is a valid dictionary word. 
    
    You may assume the dictionary does not contain duplicate words.

    Return all such possible sentences.

    
##### ***Example:***

    Input: "let", ["l", "t"]
        Output: []

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_26
 *Language: Java
 *
 */

class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        HashSet<String> dict = new HashSet<String>(wordDict);
        // assert s != null && s.length() > 0
        int n = s.length();
        List<List<Integer>> prev = new ArrayList<List<Integer>>();
        boolean[] work = new boolean[n + 1];
        work[0] = true;
        for (int i = 0; i < n; i++) {
            List<Integer> prevIndex = new ArrayList<Integer>();
            for (int j = -1; j < i; j++) {
                if (work[j + 1] && dict.contains(s.substring(j + 1, i + 1))) {
                    prevIndex.add(j);
                    work[i + 1] = true;
                }
            }
            prev.add(prevIndex);
        }
        List<String> ret = new ArrayList<String>();
        workBreakDfs(ret, s, n - 1, work, prev, new LinkedList<String>());
        return ret;
    }
    private void workBreakDfs(List<String> list, String str, int pos, boolean[] work,
                              List<List<Integer>> prev, Deque<String> cur) {
        if (!work[pos + 1]) return;
        if (pos < 0) {
            StringBuilder path = new StringBuilder();
            for (String curStr : cur) {
                path.append(curStr);
                path.append(" ");
            }
            path.deleteCharAt(path.length() - 1);
            list.add(path.toString());
        } else {
            List<Integer> prevIndex = prev.get(pos);
            for (int pre : prevIndex) {
                cur.offerFirst(str.substring(pre + 1, pos + 1));
                workBreakDfs(list, str, pre, work, prev, cur);
                cur.pollFirst();
            }
        }
    }
}



```


