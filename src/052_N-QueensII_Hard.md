

### Leetcode 52
#### [N-Queens II](https://leetcode.com/problems/n-queens-ii)

  

##### ***Problem:***

    Follow up for N-Queens problem.

    Now, instead outputting board configurations,
    return the total number of distinct solutions.
    
![ImageNQueens](https://leetcode.com/static/images/problemset/8-queens.png)
    
    
##### ***Example:***

    Input: 1
        Output: 1
    Input: 3
        Output: 0

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_01
 *Language: Java
 *
 */

public class Solution {
    private int sum = 0;
    public int totalNQueens(int n) {
        if (n <=0 || (1 < n && n < 4)) return 0;
        if (n == 1) return 1;
        //(i, j) : row : i, col : j
        //main diagonal : i + j, another : n - 1 - i + j
        char[][] queens = new char[n][n];
        for (char[] chs : queens) {
            Arrays.fill(chs, '.');
        }
        solveNQueensDFS(queens, n, 0, new boolean[n], new boolean[n],
                       new boolean[2 * n - 1], new boolean[2 * n - 1]);
        return this.sum;
    }
    private void solveNQueensDFS(char[][] queens, int n, int step, 
                                 boolean[] rowused, boolean[] colused, 
                                 boolean[] mdiagused, boolean[] adiagused) {
        if (step >= n) {
            sum++;
        } else {
            for (int i = 0; i < queens[step].length; i++) {
                if (rowused[step] || colused[i]) continue;
                if (mdiagused[i + step] || adiagused[n - 1 - step + i]) continue;
                rowused[step] = colused[i] = true;
                mdiagused[i + step] = adiagused[n - 1 - step + i] = true;
                queens[step][i] = 'Q';
                solveNQueensDFS(queens, n, step + 1, rowused, colused, mdiagused, adiagused);
                rowused[step] = colused[i] = false;
                mdiagused[i + step] = adiagused[n - 1 - step + i] = false;
                queens[step][i] = '.';
            }
        }
    }
}


```

##### *Method #2*
``` java
/*
 *Author: unknown
 *Time: 2017_08_01
 *Language: Java
 *
 */

public class Solution {
    private int sum;
    private int upperlim;
    public int totalNQueens(int n) {
        //from : 1) http://www.acmerblog.com/n-queen-3411.html
        //from : 2) http://blog.csdn.net/hackbuteer1/article/details/6657109
        //bit method
        if (n <= 0) return 0;
        // upperlim用来标记所有列都已经放置好了皇后 
        this.upperlim = (1 << n) - 1;
        // sum用来记录皇后放置成功的不同布局数
        this.sum = 0;
        test(0, 0, 0);
        return this.sum;
    }
    // 试探算法从最右边的列开始
    private void test(int row, int ld, int rd) {
        if (row != this.upperlim) {
            // row，ld，rd进行“或”运算, 求得所有可以放置皇后的列,对应位为0
            // 然后再取反后“与”上全1的数, 来求得当前所有可以放置皇后的位置, 对应列改为1  
            // 也就是求取当前哪些列可以放置皇后 
            int pos = this.upperlim & (~(row | ld | rd));
            int p;
            // pos == 0 -- 皇后没有地方可放，回溯
            while (pos != 0) {
                // 拷贝pos最右边为1的bit, 其余bit置0
                // 也就是取得可以放皇后的最右边的列
                p = pos & (~pos + 1);
                // 将pos最右边为1的bit清零
                // 也就是为获取下一次的最右可用列使用做准备
                // 程序将来会回溯到这个位置继续试探
                pos = pos - p;
                // row + p, 将当前列置1, 表示记录这次皇后放置的列
                // (ld + p) << 1, 标记当前皇后左边相邻的列不允许下一个皇后放置
                // (ld + p) >> 1, 标记当前皇后右边相邻的列不允许下一个皇后放置
                // 此处的移位操作实际上是记录对角线上的限制, 只是因为问题都化归
                // 到一行网格上来解决, 所以表示为列的限制就可以了
                // 显然,随着移位
                // 在每次选择列之前进行, 原来N×N网格中某个已放置的皇后针对其对角线
                // 上产生的限制都被记录下来
                test(row | p, (ld | p) << 1, (rd | p) >> 1);
            }
        } else {
            // row的所有位都为1，即找到了一个成功的布局
            this.sum++;
        }
    }
}

```


