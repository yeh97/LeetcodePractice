


### Leetcode 187
#### [Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences)

  

##### ***Problem:***

	All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, 
	for example: "ACGAATTCCG". 
	When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.
	Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

##### ***Example:***

    Input: "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
        Output: ["AAAAACCCCC", "CCCCCAAAAA"]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_07
 *Language: Java
 *
 */

class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        // 2018/2/7 : 41ms
        // hash + set
        List<String> res = new ArrayList<String>();
        if (s == null || s.length() < 10) return res;
        // (s[i] - 'A' + 1) % 5 --> A:1, C:3, G:2, T:0
        // 0xfffff = (1<<20) - 1 = 1048575, Integer.MAX_VALUE = 0xffffffff
        int val = 0;
        Set<Integer> hashval_1 = new HashSet<Integer>();
        Set<Integer> hashval_2 = new HashSet<Integer>();
        for (int i = 0; i < s.length(); i++) {
            val = ((val << 2) | ((s.charAt(i) - 'A' + 1) % 5)) & 0xfffff;
            if (i < 9) continue; // not a 10-letter-long sequence
            if (!hashval_1.add(val) && hashval_2.add(val)) {
                res.add(s.substring(i - 9, i + 1));
            }
        }
        return res;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_02_07
 *Language: Java
 *
 */

class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        // 2018/2/7 : 11ms
        // hash + bit
        List<String> res = new ArrayList<String>();
        if (s == null || s.length() < 10) return res;
        // (s[i] - 'A' + 1) % 5 --> A:1, C:3, G:2, T:0
        // 0xfffff = (1<<20) - 1 = 1048575, Integer.MAX_VALUE = 0xffffffff
        int val = 0;
        byte[] hashval = new byte[1 << 20];
        char[] str = s.toCharArray();
        for (int i = 0; i < 9; i++) {
            val = (val << 2) | ((str[i] - 'A' + 1) % 5);
        }
        for (int i = 9; i < str.length; i++) {
            val = ((val << 2) | ((str[i] - 'A' + 1) % 5)) & 0xfffff;
            if (hashval[val] == 1) res.add(new String(str, i - 9, 10));
            if (hashval[val] < 2) hashval[val]++;
        }
        return res;
    }
}

```








