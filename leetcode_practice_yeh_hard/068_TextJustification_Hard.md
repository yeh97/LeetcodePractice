

### Leetcode 68
#### [Text Justification](https://leetcode.com/problems/text-justification)

  

##### ***Problem:***

    Given an array of words and a length L, 
    format the text such that each line has exactly L characters and 
    is fully (left and right) justified.
    
    You should pack your words in a greedy approach; 
    that is, pack as many words as you can in each line. 
    Pad extra spaces ' ' when necessary so that each line has exactly L characters.
    
    Extra spaces between words should be distributed as evenly as possible. 
    If the number of spaces on a line do not divide evenly between words, 
    the empty slots on the left will be assigned more spaces than the slots on the right.
    
    For the last line of text, 
    it should be left justified and no extra space is inserted between words.

##### ***Example:***

    Input: ["attt", "to", "f", "a", "sss"], 4
        Output: ["attt", "to f", "a   ", "sss "]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_06
 *Language: Java
 *
 */

public class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        //assert: max(words[i].length()) <= maxWidth
        List<String> ret = new LinkedList<String>();
        if (words == null || words.length == 0) return ret;
        int addl = 0;
        int addLength = words[0].length();
        int addString = 0;
        int extraSpace = 0;
        for (int i = 1; i < words.length; i++) {
            if (addLength + words[i].length() + 1 <= maxWidth) {
                addLength += words[i].length() + 1;
            } else {
                //add [addl, i)
                addString = i - addl;
                extraSpace = maxWidth - addLength + addString - 1;
                StringBuilder line = new StringBuilder();
                line.append(words[addl]);
                if (addString < 2) {
                    //only one element
                    //guarantee maxWidth length
                    for (int j = extraSpace; j > 0; j--) {
                        line.append(" ");
                    }
                } else {
                    for (int j = addl + 1; j < i; j++) {
                        for (int k = (extraSpace + i - j - 1) / (addString - 1); k > 0; k--) {
                            line.append(" ");
                        }
                        line.append(words[j]);
                    }
                }
                ret.add(line.toString());
                addl = i;
                addLength = words[i].length();
            }          
        }
        addString = words.length - addl;
        extraSpace = maxWidth - addLength + addString - 1;
        StringBuilder line = new StringBuilder();
        line.append(words[addl]);
        for (int j = addl + 1; j < words.length; j++) {
            line.append(" ");
            extraSpace--;
            line.append(words[j]);
        }
        for (int j = extraSpace; j > 0; j--) {
            line.append(" ");
        }
        ret.add(line.toString());
        return ret;
    }
}

```


