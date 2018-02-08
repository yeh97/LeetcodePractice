

### Leetcode 56
#### [Merge Intervals](https://leetcode.com/problems/merge-intervals)

  

##### ***Problem:***

    Given a collection of intervals, merge all overlapping intervals.
    
##### ***Note:***

    1) the length of input may be 0
    
##### ***Example:***

    Input: [1,3],[2,6],[8,10],[15,18]
        Output: [1,6],[8,10],[15,18]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_02
 *Language: Java
 *
 */

/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    private Class<Interval> intervalType;
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> ret = new LinkedList<Interval>();
        if (intervals == null || intervals.size() == 0) {
            return ret;
        }

        //sorted from small to big number
        Comparator<Interval> cmp = new Comparator<Interval>() {
            public int compare(Interval a, Interval b) {
                //assert(a!=null && b!=null)
                if(a.start < b.start) return -1;
                else if(a.start > b.start) return 1;
                else return 0;
            }
        };
        Collections.sort(intervals, cmp);
        
        Iterator iter = intervals.iterator();
        Interval t = (Interval) iter.next();
        int start = t.start;
        int end = t.end;
        while (iter.hasNext()) {
            t = (Interval) iter.next();
            if (t.start > end) {
                //t belong to another interval
                ret.add(new Interval(start, end));
                start = t.start;
                end = t.end;
            } else if (t.end > end) {
                end = t.end;
            }
        }
        ret.add(new Interval(start, end));
        return ret;
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_02
 *Language: Java
 *
 */

/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> ret = new LinkedList<Interval>();
        if (intervals == null || intervals.size() == 0) {
            return ret;
        }
        //similar to Method #1
        int n = intervals.size();
        int[] starts = new int[n];
        int[] ends = new int[n];
        Iterator iter = intervals.iterator();
        Interval t = null;
        for (int i = 0; iter.hasNext(); i++) {
            t = (Interval) iter.next();
            starts[i] = t.start;
            ends[i] = t.end;
        }
        Arrays.sort(starts);
        Arrays.sort(ends);
        
        int startId = 0;
        for (int i = 0; i < n; i++) {
            //if [s_1, e_1]...[s_i, e_i] is overlapping
            //[s_i+1, e_i+1] not a member
            //<--> s_i+1 > e_i
            //<-->starts[i + 1] > ends[i]
            if (i == n - 1 || starts[i + 1] > ends[i]) {
                ret.add(new Interval(starts[startId], ends[i]));
                startId = i + 1;
            }
        }
        return ret;
    }
}
```

