


### Leetcode 179
#### [Largest Number](https://leetcode.com/problems/largest-number)

  

##### ***Problem:***

	Given a list of non negative integers, arrange them such that they form the largest number.

##### ***Example:***

    Input: [3, 30, 34, 5, 9, 0]
        Output: 95343300


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_06
 *Language: Java
 *
 */

class Solution {
    class Data implements Comparable<Data> {
        public int d, n;
        public Data(int num) {
            this.d = num;
            // min(n) = 10^^1
            for (this.n = 10; d >= n; n *= 10) /**/;
        }
        @Override
        public int compareTo(Data t) {
            // sorted big -> small
            long num1 = ((long) d) * t.n + t.d;
            long num2 = ((long) t.d) * n + d;
            return num1 > num2 ? -1 : 1;
        }
    }
    public String largestNumber(int[] nums) {
        // 2018/2/6 : 108ms
        // string a, b, sort it by a + b > b + a
        if (nums == null || nums.length == 0) return "";
        Data[] data = new Data[nums.length];
        for (int i = 0; i < nums.length; i++) {
            data[i] = new Data(nums[i]);
        }
        Arrays.sort(data);
        // if max(data) == 0, every elem is 0
        if (data[0].d == 0) return "0";
        StringBuilder res = new StringBuilder("");
        for (int i = 0; i < data.length; i++) {
            res.append(String.valueOf(data[i].d));
        }
        return res.toString();
    }
}

```





