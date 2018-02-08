

### Leetcode 149
#### [Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line)

  

##### ***Problem:***

    Given n points on a 2D plane, 
    find the maximum number of points that lie on the same straight line.
    
##### ***Example:***

    Input: [[1,2],[1,2],[5,6],[7,4]]
        Output: 3


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_28
 *Language: Java
 *
 */

/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
class Solution {
    public int maxPoints(Point[] points) {
	    // O(n^3)
	    // 2018/1/28 : 20ms
        if (points == null) return 0;
        int size = points.length;
        if (size < 3) return size;
        int res = 0;
        boolean[] used = new boolean[size];
        for (int i = 0; i < size; i++) {
            if (used[i]) continue;
            used[i] = true;
            int dup = 1; // duplicate time (include points[i])
            for (int j = i + 1; j < size; j++) {
                if (points[i].x == points[j].x && points[i].y == points[j].y) {
                    dup++;
                    used[j] = true;
                }
            }
            for (int j = i + 1; j < size; j++) {
                if (used[j]) continue;
                int cnt = 1; // num of point (include points[j])
                for (int k = j + 1; k < size; k++) {
                    if (used[k]) continue;
                    if (sameLine(points[i].x, points[i].y, 
                                 points[j].x, points[j].y, 
                                 points[k].x, points[k].y)) {
                        cnt++; // add points[k]
                    }
                }
                res = Math.max(res, cnt + dup);
            }
            res = Math.max(res, dup);
        }
        return res;
    }
    private boolean sameLine(long x1, long y1, long x2, long y2, long x3, long y3) {
        // 2 * area(triangle_ABC) == 0 <--> same straight line
        return (x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2)) == 0;
    }
}

```

