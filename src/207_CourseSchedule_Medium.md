


### Leetcode 207
#### [Course Schedule](https://leetcode.com/problems/course-schedule)

  

##### ***Problem:***

    There are a total of n courses you have to take, labeled from 0 to n-1.
    Some courses may have prerequisites,
    for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]
    Given the total number of courses and a list of prerequisite pairs,
    is it possible for you to finish all courses?

##### ***Example:***

    Input: 1, [[1,0],[0,1]]
        Output: false

##### *Method #1*
``` python
/*
 *Author: yeh
 *Time: 2018_07_03
 *Language: Python3
 *
 */

class Solution:
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        # Kahn + bfs
        # https://en.wikipedia.org/wiki/Topological_sorting#Kahn's_algorithm
        # node : num of inNode, List of outNode
        forest = [[0, []] for _ in range(numCourses)]
        for (inNode, outNode) in prerequisites:
            forest[inNode][0] += 1
            forest[outNode][1].append(inNode)
        queue = [ii for ii in range(numCourses) if forest[ii][0] == 0]
        while queue:
            curNode = queue.pop(0)
            numCourses -= 1
            for nextNode in forest[curNode][1]:
                forest[nextNode][0] -= 1
                if forest[nextNode][0] == 0:
                    queue.append(nextNode)
        return 0 == numCourses

```

