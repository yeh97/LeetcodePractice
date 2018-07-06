


### Leetcode 210
#### [Course Schedule II](https://leetcode.com/problems/course-schedule-ii)


##### ***Problem:***

    There are a total of n courses you have to take, labeled from 0 to n-1.

    Some courses may have prerequisites, for example to take course 0 you have to first take course 1,
    which is expressed as a pair: [0,1]

    Given the total number of courses and a list of prerequisite pairs,
    return the ordering of courses you should take to finish all courses.

    There may be multiple correct orders, you just need to return one of them.
    If it is impossible to finish all courses, return an empty array.

##### ***Example:***

    Input: 4, [[1,0],[2,0],[3,1],[3,2]]
        Output: [0,1,2,3] or [0,2,1,3]

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_03
 *Language: Python3
 *
 */

class Solution:
    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """
        # Kahn
        forest = [[0, []] for _ in range(numCourses)]
        for (inNode, outNode) in prerequisites:
            forest[inNode][0] += 1
            forest[outNode][1].append(inNode)
        queue = [ii for ii in range(numCourses) if forest[ii][0] == 0]
        sortedList = []
        while queue:
            curNode = queue.pop(0)
            sortedList.append(curNode)
            numCourses -= 1
            for nextNode in forest[curNode][1]:
                forest[nextNode][0] -= 1
                if forest[nextNode][0] == 0:
                    queue.append(nextNode)
        return sortedList if 0 == numCourses else []

```

