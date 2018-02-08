

### Leetcode 30
#### [Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words)

  

##### ***Problem:***

    You are given a string, s, 
    and a list of words, words, 
    that are all of the same length. 
    
    Find all starting indices of substring(s) in s 
    that is a concatenation of each word in words 
    exactly once and without any intervening characters.
    
##### ***Note:***

    1) order does not matter
    2) it's possible: 
        words[i]==words[j] when i!=j


##### ***Example:***

    Input: "barfoothefoobarman", 
            ["foo", "bar"]
        Output: [0, 9]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_14
 *Language: Java
 *
 */

public class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> ret = new LinkedList<Integer>();
        if(words==null || words.length==0 || s==null || s.length()==0) return ret;
        //every word has same length
        int wordlen = words[0].length();
        int slen = s.length();
        if(wordlen*words.length > slen) return ret;
        HashMap<String, Integer> wordsMap = new HashMap<String, Integer>();
        HashMap<String, Integer> matchMap = new HashMap<String, Integer>();
        for(String word : words) {
            add(wordsMap, word);
        }
        //the left of splid window
        int windowLeft;
        //the left of the matched Stirng in s
        int matchLeft;
        //matched times
        int count;
        String matchstr;
        String windowstr;
        for(int i=0; i<wordlen; i++) {
            matchMap.clear();
            matchLeft = i;
            windowLeft = i;
            count = 0;
            while(matchLeft <= slen-wordlen) {
                matchstr = s.substring(matchLeft, matchLeft+wordlen);
                if(wordsMap.containsKey(matchstr)) {
                    add(matchMap, matchstr);
                    if(matchMap.get(matchstr) <= wordsMap.get(matchstr)) {
                        count++;
                    }else{
                        while(matchMap.get(matchstr) > wordsMap.get(matchstr)) {
                            windowstr = s.substring(windowLeft, windowLeft+wordlen);
                            matchMap.put(windowstr, matchMap.get(windowstr)-1);
                            if(matchMap.get(windowstr) < wordsMap.get(windowstr)) {
                                count--;
                            }
                            windowLeft += wordlen;
                        }
                    }
                    if(count == words.length) {
                        ret.add(windowLeft);
                        windowstr = s.substring(windowLeft, windowLeft+wordlen);
                        matchMap.put(windowstr, matchMap.get(windowstr)-1);
                        count--;
                        windowLeft += wordlen;
                    }
                }else{
                    matchMap.clear();
                    count = 0;
                    windowLeft = matchLeft + wordlen;
                }
                matchLeft += wordlen;
            }
        }
        return ret;
    }
    private static void add(HashMap<String, Integer> map, String word) {
        if(map.containsKey(word)) {
            map.put(word, map.get(word)+1);
        }else{
            map.put(word, 1);
        }
    }
}

```
