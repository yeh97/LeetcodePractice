

### Leetcode 17
#### [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number)

    Given a digit string, 
    return all possible letter combinations that the number could represent.
    
    A mapping of digit to letters (just like on the telephone buttons) is given below.
    
![Letter-Combinations-of-a-Phone-Number](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

    
**Example:**

    Input:Digit string "23"
    Output: ["ad", "ae", "af", "bd", 
            "be", "bf", "cd", "ce", "cf"].

**Note:**

    Although the above answer is in lexicographical order, 
    your answer could be in any order you want.

``` java
/*
 *Author: yeh
 *Time: 2017_07_10
 *Language: Java
 *
 */

public class Solution {
    //the string number could represent
    public static final String[] map = {"", "", "abc", "def", "ghi", "jkl", "mno",
                                        "pqrs", "tuv", "wxyz"};
    public List<String> letterCombinations(String digits) {
        List<String> ret = new LinkedList<String>();
        if(digits==null || digits.length()==0) return ret;
        String letters = "";
        //dfs
        letterCombinationsHelper(ret, letters, digits, 0);
        return ret;
    }
    private void letterCombinationsHelper(List<String> list, String letters, 
                                          String digits, int index) {
        //assert(list!=null && letters!=null && digits!=null && index>=0);
        if(index>=digits.length()) {
            list.add(letters);
            return;
        }
        int num = digits.charAt(index)-'0';
        //assert(num>=0 && num<=9);
        int size = map[num].length();
        for(int i=0; i<size; i++) {
            letterCombinationsHelper(list, 
                                     letters+map[num].charAt(i), digits, index+1);
        }
    }
}

```
