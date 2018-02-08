


### Leetcode 200
#### [Number of Islands](https://leetcode.com/problems/number-of-islands)

  

##### ***Problem:***

	Given a 2d grid map of '1's (land) and '0's (water), count the number of islands.
	An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.
	You may assume all four edges of the grid are all surrounded by water.
	
##### ***Example:***

    Input: [['1','0'],['0','1']]
        Output: 2

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_08
 *Language: Java
 *
 */

class Solution {
    public int numIslands(char[][] grid) {
        // 2018/2/8 : 8ms
        // union-find sets
        // union '1', return num of set with '1'
        if (grid == null || grid.length == 0) return 0;
        if (grid[0] == null || grid.length == 0) return 0;
        int m = grid.length;
        int n = grid[0].length;
        int[] parents = new int[m * n];
        for (int i = 0; i < parents.length; i++) {
            parents[i] = i;
        }
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != '1') continue;
                if (i > 0 && grid[i - 1][j] == '1') Union((i - 1) * n + j, i * n + j, parents);
                if (j > 0 && grid[i][j - 1] == '1') Union(i * n + j - 1, i * n + j, parents);
            }
        }
        // get num of islands
        int res = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != '1') continue;
                int index = i * n + j;
                if (parents[index] == index) res++;
            }
        }
        return res;
    }
    private int Find(int i, int[] parents) {
        return parents[i] == i ? i : (parents[i] = Find(parents[i], parents));
    }
    private void Union(int i, int j, int[] parents) {
        int a = Find(i, parents);
        int b = Find(j, parents);
        if (a != b) parents[a] = b;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_02_08
 *Language: Java
 *
 */

class Solution {
    public int numIslands(char[][] grid) {
        // 2018/2/8 : 6ms
        // dfs
        if (grid == null || grid.length == 0) return 0;
        if (grid[0] == null || grid.length == 0) return 0;
        int m = grid.length;
        int n = grid[0].length;
        int res = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != '1') continue;
                DFS(grid, i, j);
                res++;
            }
        }
        return res;
    }
    private void DFS(char[][] grid, int i, int j) {
        if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length) return;
        if (grid[i][j] != '1') return;
        grid[i][j] = '0';
        DFS(grid, i - 1, j); 
        DFS(grid, i + 1, j);
        DFS(grid, i, j - 1); 
        DFS(grid, i, j + 1);
    }
}


```

