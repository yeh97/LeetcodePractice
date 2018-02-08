

### Leetcode 127
#### [Word Ladder](https://leetcode.com/problems/word-ladder)

  

##### ***Problem:***

    Given two words (beginWord and endWord), 
    and a dictionary's word list, 
    find the length of shortest transformation sequence from beginWord to endWord, 
    such that:
    1) Only one letter can be changed at a time
    2) Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

##### ***Note:***

    1) Return 0 if there is no such transformation sequence.
    2) All words have the same length.
    3) All words contain only lowercase alphabetic characters.
    4) You may assume no duplicates in the word list.
    5) You may assume beginWord and endWord are non-empty and are not the same.
    6) if endWord is not in wordList, you can't find such transformation sequence.
    
##### ***Example:***

    Input: "ab", "bc", ["ac", "bc", "ad"]
        Output: 3

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_22
 *Language: Java
 *
 */

class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        // similar to : leetcode 126
        // BFS
        HashSet<String> wordSet = new HashSet<String>(wordList);
        if (!wordSet.contains(endWord)) return 0;
        
        HashSet<String> fwd = new HashSet<String>();
        HashSet<String> bck = new HashSet<String>();
        fwd.add(beginWord);
        bck.add(endWord);
        wordSet.remove(beginWord);
        wordSet.remove(endWord);
        
        return Math.max(0, 2 + findLadder(fwd, bck, wordSet, true));
    }
    // findLadder : return the number of node between fwd and bck
    private int findLadder(Set<String> fwd, Set<String> bck, Set<String> wordSet, boolean dire) {
        
        // can't find path
        if (fwd.size() == 0 || bck.size() == 0) return Integer.MIN_VALUE;
        
        if (fwd.size() > bck.size()) {
            return findLadder(bck, fwd, wordSet, !dire);
        }
        
        Set<String> fwdNew = new HashSet<String>();
        for (String str : fwd) {
            char[] strs = str.toCharArray();
            for (int i = 0; i < strs.length; i++) {
                char old = strs[i];
                
                for (char ch = 'a'; ch <= 'z'; ch++) {
                    if (old == ch) continue;
                    strs[i] = ch;
                    String strt = new String(strs);
                    if (bck.contains(strt)) {
                        // find shortest path
                        return 0;
                    }
                    if (wordSet.contains(strt)) {
                        fwdNew.add(strt);
                    }
                }
                
                strs[i] = old;
            }
        }
        wordSet.removeAll(fwdNew);
        return 1 + findLadder(fwdNew, bck, wordSet, dire);
    }
}

```


