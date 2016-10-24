Clone Graph
===



Problem
-------

Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.

How we serialize an undirected graph:

Nodes are labeled uniquely.

We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
As an example, consider the serialized graph {0,1,2#1,2#2,2}.

The graph has a total of three nodes, and therefore contains three parts as separated by #.

First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
Second node is labeled as 1. Connect node 1 to node 2.
Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
Visually, the graph looks like the following:

       1
      / \
     /   \
    0 --- 2
         / \
         \_/

Example
-------

return a deep copied graph.

Note
---------

Challenge
---------

Solution
--------

Code
----

    #!java
    /**
     * Definition for undirected graph.
     * class UndirectedGraphNode {
     *     int label;
     *     ArrayList<UndirectedGraphNode> neighbors;
     *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
     * };
     */
    public class Solution {
        
        private Map<Integer, UndirectedGraphNode> map = new HashMap<>();
        
        /**
         * @param node: A undirected graph node
         * @return: A undirected graph node
         */
        public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
            
            if (node == null) {
                return null;
            }
        
            if (map.containsKey(node.label)) {
                return map.get(node.label);
            } 
            
            UndirectedGraphNode newNode = new UndirectedGraphNode(node.label);
            map.put(node.label, newNode);
            for (UndirectedGraphNode neighbor : node.neighbors) {
                newNode.neighbors.add(cloneGraph(neighbor));
            }
            
            return newNode;
        }
    }