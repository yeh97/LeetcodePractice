

### Leetcode 57
#### [Insert Interval](https://leetcode.com/problems/insert-interval)

  

##### ***Problem:***

    Given a set of non-overlapping intervals, 
    insert a new interval into the intervals (merge if necessary).
    
    You may assume that the intervals were 
    initially sorted according to their start times.
    
    
##### ***Example:***

    Input: [[1,3],[6,9]], [2,5]
        Output: [[1,5],[6,9]]

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
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        if (newInterval == null) {
            return intervals == null ? new LinkedList<Interval>() : intervals;
        } else if (intervals == null) {
            List<Interval> ret = new LinkedList<Interval>();
            ret.add(new Interval(newInterval.start, newInterval.end));
            return ret;
        } else if (intervals.size() == 0) {
            intervals.add(new Interval(newInterval.start, newInterval.end));
            return intervals;
        }
        
        ListIterator iter = intervals.listIterator();
        Interval t = null;
        int newStart = newInterval.start;
        int newEnd = newInterval.end;
        while (iter.hasNext()) {
            t = (Interval) iter.next();
            if (t.start > newEnd) {
                iter.previous();
                iter.add(new Interval(newStart, newEnd));
                return intervals;
            } else {
                if (t.end < newStart) {
                    //not change
                    continue;
                } else{
                    //overlapping
                    newStart = Math.min(t.start, newStart);
                    newEnd = Math.max(t.end, newEnd);
                    iter.remove();
                }
            }
        }
        iter.add(new Interval(newStart, newEnd));
        return intervals;
    }
}


```


