

### Leetcode 133
#### [Clone Graph](https://leetcode.com/problems/clone-graph)

  

##### ***Problem:***

    Clone an undirected graph. 
    Each node in the graph contains a label and a list of its neighbors

    
##### ***Example:***

    Input: {1}
        Output: {1}

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_23
 *Language: Java
 *
 */

/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) return null;
        return cloneGraph(node, new HashMap<UndirectedGraphNode, UndirectedGraphNode>());
    }
    private UndirectedGraphNode cloneGraph(UndirectedGraphNode node, 
                                           Map<UndirectedGraphNode, UndirectedGraphNode> map) {
        UndirectedGraphNode newNode = new UndirectedGraphNode(node.label);
        List<UndirectedGraphNode> list = newNode.neighbors;
        map.put(node, newNode);
        for (UndirectedGraphNode next : node.neighbors) {
            if (map.containsKey(next)) {
                list.add(map.get(next));
            } else {
                list.add(cloneGraph(next, map));
            }
        }
        return newNode;
    }
}


```


