

### Leetcode 118
#### [Pascal's Triangle](https://leetcode.com/problems/pascals-triangle)

  

##### ***Problem:***

    Given numRows, 
    generate the first numRows of Pascal's triangle.
    

##### ***Example:***

    Input: 2
        Output: [[1], [1,1]]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_14
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ret = new ArrayList<>();
        if (numRows < 1) return ret;
        List<Integer> preLine = null;
        List<Integer> line = null;
        line = new ArrayList<Integer>();
        line.add(1);
        ret.add(line);
        for (int i = 1; i < numRows; i++) {
            preLine = ret.get(i - 1);
            line = new ArrayList<Integer>();
            line.add(1);
            for (int j = 1; j < i; j++) {
                line.add(preLine.get(j - 1) + preLine.get(j));
            }
            line.add(1);
            ret.add(line);
        }
        return ret;
    }
}


```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_14
 *Language: Java
 *
 */

public class Solution {
    public List<List<Integer>> generate(int numRows) {
        if (numRows < 1) return new ArrayList<>();
        int[][] num = new int[numRows][];
        for (int i = 0; i < numRows; i++) {
            num[i] = new int[i + 1];
        }
        for (int i = 0; i < numRows; i++) {
            num[i][0] = num[i][i] = 1;
            for (int j = 1; j < i; j++) {
                num[i][j] = num[i - 1][j - 1] + num[i - 1][j];
            }
        }
        return (List) Arrays.asList(num);
    }
}

```


