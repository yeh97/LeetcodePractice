

### Leetcode 126
#### [Word Ladder II](https://leetcode.com/problems/word-ladder-ii)

  

##### ***Problem:***

    Given two words (beginWord and endWord), 
    and a dictionary's word list, 
    find all shortest transformation sequence(s) from beginWord to endWord, such that:
    1) Only one letter can be changed at a time
    2) Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

##### ***Note:***

    1) Return an empty list if there is no such transformation sequence.
    2) All words have the same length.
    3) All words contain only lowercase alphabetic characters.
    4) You may assume no duplicates in the word list.
    5) You may assume beginWord and endWord are non-empty and are not the same.
    6) if endWord is not in wordList, you can't find such transformation sequence.
    
##### ***Example:***

    Input: "ab", "bc", ["ac", "bc", "ad"]
        Output: [["ab", "ac", "bc"]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_22
 *Language: Java
 *
 */

public class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        // solution time : 773ms
        List<List<String>> ret = new ArrayList<List<String>>();
        wordList = new ArrayList<String>(wordList);
        // wordList.get(endIndex - 1) == endWord
        int endIndex = 0;
        for (endIndex = wordList.size(); endIndex > 0; endIndex--) {
            if (endWord.equals(wordList.get(endIndex - 1))) break;
        }
        if (endIndex <= 0) return ret;
        int n = wordList.size() + 1;
        // trans status
        boolean[][] trans = new boolean[n][n];
        for (int j = wordList.size(); j > 0; j--) {
            trans[j][0] = trans[0][j] = getStatus(beginWord, wordList.get(j - 1));
        }
        for (int i = n - 1; i > 0; i--) {
            String stri = wordList.get(i - 1);
            for (int j = n - 1; j > i; j--) {
                trans[j][i] = trans[i][j] = getStatus(stri, wordList.get(j - 1));
            }
        }
        // depth of word in wordList
        int[] depth = getDepth(trans, n, endIndex);
        List<String> solution = new ArrayList<String>();
        solution.add(beginWord);
        findLaddersDFS(trans, depth, 0, n, endIndex, wordList, ret, solution);
        return ret;
    }
    private int[] getDepth(boolean[][] trans, int n, int end) {
        int[] depth = new int[n];
        Queue<Integer> q = new LinkedList<Integer>();
        q.add(0);
        while(!q.isEmpty()) {
            int t = q.remove();
            for (int i = n - 1; i > 0; i--) {
                if (trans[t][i] && depth[i] == 0) {
                    depth[i] = depth[t] + 1;
                    q.add(i);
                }
            }
        }
        int[] path = new int[n];
        path[end] = depth[end];
        q.add(end);
        while(!q.isEmpty()) {
            int t = q.remove();
            for (int i = n - 1; i > 0; i--) {
                if (trans[t][i] && depth[t] == depth[i] + 1) {
                    path[i] = depth[i];
                    q.add(i);
                }
            }
        }
        return path;
    }
    private void findLaddersDFS(boolean[][] trans, int[] used, int cur, int n,
                                int endIndex, List<String> wordList,
                               List<List<String>> list, List<String> solution) {
        if (cur == endIndex) {
            list.add(new ArrayList<String>(solution));
        } else {
            String str = null;
            int length = solution.size();
            for (int i = n - 1; i > 0; i--) {
                if (used[i] != length || !trans[cur][i]) continue;
                str = wordList.get(i - 1);
                solution.add(str);
                findLaddersDFS(trans, used, i, n, endIndex, wordList, list, solution);
                solution.remove(solution.size() - 1);
            }
        }
    }
    private boolean getStatus(String s1, String s2) {
        // if (s1 == null || s2 == null) return false;
        // if (s1.length() != s2.length()) return false;
        boolean diff = false;
        for (int i = s1.length() - 1; i >= 0; i--) {
            if (s1.charAt(i) == s2.charAt(i)) continue;
            if (diff) return false;
            diff = true;
        }
        return diff;
    }
}

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_22
 *Language: Java
 *
 */

public class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        // contain only lowercase alphabetic characters
        // --> O(26*n) < O(n^2) --> O(kn^2) --> O(kn)
        // HashSet : get element need O(1) time
        // solution time : 38ms
        // BFS + DFS
        List<List<String>> path = new ArrayList<List<String>>();
        HashSet<String> wordSet = new HashSet<String>(wordList);
        if (!wordSet.contains(endWord)) return path;
        
        HashMap<String, List<String>> strLadder = new HashMap<String, List<String>>();
        HashSet<String> fwd = new HashSet<String>();
        HashSet<String> bck = new HashSet<String>();
        fwd.add(beginWord);
        bck.add(endWord);
        wordSet.remove(beginWord);
        wordSet.remove(endWord);
        
        findLadder(fwd, bck, wordSet, true, strLadder);
        
        List<String> curPath = new ArrayList<String>();
        curPath.add(beginWord);
        pathDFS(beginWord, endWord, strLadder, curPath, path);
        return path;
    }
    private void findLadder(Set<String> fwd, Set<String> bck, Set<String> wordSet,
                            boolean dire, Map<String, List<String>> strLadder) {
        // find link : fwd <--> bck
        // if dire == true, fwd --> bck
        if (fwd.size() == 0 || bck.size() == 0) return;
        if (fwd.size() > bck.size()) {
            findLadder(bck, fwd, wordSet, !dire, strLadder);
            return;
        }
        // find link ? 
        // true : has found shortest path
        boolean find = false;
        // fwdNew : next level fwd
        // if can't find link fwd <--> bck
        // --> has not found shorest path
        // --> need next level string to find path
        Set<String> fwdNew = new HashSet<String>();
        for (String str : fwd) {
            char[] strs = str.toCharArray();
            for (int i = 0; i < strs.length; i++) {
                char old = strs[i];
                // find new string can convert from str
                for (char ch = 'a'; ch <= 'z'; ch++) {
                    if (old == ch) continue;
                    strs[i] = ch;
                    String strt = new String(strs);
                    if (bck.contains(strt)) {
                        find = true;
                        addLadder(str, strt, dire, strLadder);
                    } else if (!find && wordSet.contains(strt)) {
                        fwdNew.add(strt);
                        addLadder(str, strt, dire, strLadder);
                    }
                }
                strs[i] = old;
            }
        }
        if (find) return;
        wordSet.removeAll(fwdNew);
        findLadder(fwdNew, bck, wordSet, dire, strLadder);
    }
    private void addLadder(String s, String t, boolean dire, Map<String, List<String>> strLadder) {
        if (dire) {
            addLadder(s, t, strLadder);
        } else {
            addLadder(t, s, strLadder);
        }
    }
    private void addLadder(String s, String t, Map<String, List<String>> strLadder) {
        // s --> t
        if (strLadder.containsKey(s)) {
            strLadder.get(s).add(t);
        } else {
            List<String> l = new ArrayList<String>();
            l.add(t);
            strLadder.put(s, l);
        }
    }
    private void pathDFS(String s, String e, Map<String, List<String>> strLadder, 
                         List<String> curPath, List<List<String>> list) {
        if (s.equals(e)) {
            list.add(new ArrayList<String>(curPath));
        } else {
            if (!strLadder.containsKey(s)) return;
            for (String str : strLadder.get(s)) {
                curPath.add(str);
                pathDFS(str, e, strLadder, curPath, list);
                curPath.remove(curPath.size() - 1);
            }
        }
    }
}



```


