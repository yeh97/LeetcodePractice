


### Leetcode 165
#### [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers)

  

##### ***Problem:***

    Compare two version numbers version1 and version2.
	If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.
	You may assume that the version strings are non-empty and contain only digits and the . character.
	The . character does not represent a decimal point and is used to separate number sequences.
    
##### ***Example:***

    Input: "0.1.01.2","0.01.1.02.0.1"
        Output: -1


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_02
 *Language: Java
 *
 */

class Solution {
    public int compareVersion(String version1, String version2) {
        // 2018/2/2 : 2ms
        // assert not-empty string, contain only digits and '.'
        int[] v1 = versionToIntegerArray(version1);
        int[] v2 = versionToIntegerArray(version2);
        int length = Math.min(v1.length, v2.length);
        for (int i = 0; i < length; i++) {
            if (v1[i] == v2[i]) continue;
            return v1[i] > v2[i] ? 1 : -1;
        }
        int[] v = v1.length > length ? v1 : (v2.length > length ? v2 : null);
        if (v == null) return 0;
        for (int i = length; i < v.length; i++) {
            if (v[i] == 0) continue;
            return v == v1 ? 1 : -1;
        }
        return 0;
    }
    private int[] versionToIntegerArray(String version) {
        String[] v = version.split("\\.");
        int[] nums = new int[v.length];
        for (int i = 0; i < v.length; i++) {
            nums[i] = Integer.parseInt(v[i]);
        }
        return nums;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_02_02
 *Language: Java
 *
 */

class Solution {
    public int compareVersion(String version1, String version2) {
        // 2018/2/2 : 3ms
        // assert not-empty string, contain only digits and '.'
        int[] v1 = versionToIntegerArray(version1);
        int[] v2 = versionToIntegerArray(version2);
        for (int i = 0; i < v1.length || i < v2.length; i++) {
            int num1 = i < v1.length ? v1[i] : 0;
            int num2 = i < v2.length ? v2[i] : 0;
            if (num1 == num2) continue;
            return num1 > num2 ? 1 : -1;
        }
        return 0;
    }
    private int[] versionToIntegerArray(String version) {
        String[] v = version.split("\\.");
        int[] nums = new int[v.length];
        for (int i = 0; i < v.length; i++) {
            nums[i] = Integer.parseInt(v[i]);
        }
        return nums;
    }
}

```

##### *Method #3*
``` java
/*
 *Author: yeh
 *Time: 2018_02_02
 *Language: Java
 *
 */

class Solution {
    public int compareVersion(String version1, String version2) {
        // 2018/2/2 : 0ms
        // assert not-empty string, contain only digits and '.'
        char[] v1 = version1.toCharArray();
        char[] v2 = version2.toCharArray();
        int i = 0, j = 0;
        while (i < v1.length || j < v2.length) {
            int num1 = 0, num2 = 0;
            for (/**/; i < v1.length && v1[i] != '.'; i++) {
                num1 = num1 * 10 + (v1[i] - '0');
            }
            for (/**/; j < v2.length && v2[j] != '.'; j++) {
                num2 = num2 * 10 + (v2[j] - '0');
            }
            if (num1 != num2) return num1 > num2 ? 1 : -1;
            i++;
            j++;
        }
        return 0;
    }
}

```


