


### Leetcode 214
#### [Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome)


##### ***Problem:***

    Given a string s, you are allowed to convert it to a palindrome by adding characters in front of it.
    Find and return the shortest palindrome you can find by performing this transformation.

##### ***Example:***

    Input: "aacecaaa"
        Output: "aaacecaaa"

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_04
 *Language: Python3
 *
 */

class Solution:
    def shortestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        j = 0
        for i in range(len(s))[::-1]:
            j += (s[i] == s[j])
        return s[::-1] if j == len(s) else s[j:][::-1] + self.shortestPalindrome(s[:j]) + s[j:]

```


