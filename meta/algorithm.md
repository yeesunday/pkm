## BFS

Breadth-first Search (BFS) 广度优先搜索，是一种盲目搜索法，目的是系统地展开并检查图中的所有节点，以找寻结果。换句话说，它并不考虑结果的可能地址，彻底地搜索整张图，直到找到结果为止。

可以应用的场景：
* 查找图中所有连接组件（Connected Component）。一个连接组件是图中的最大相连子图。
* 查找连接组件中的所有节点。
* 查找非加权图中任两点的最短路径。
* 测试一图是否为二分图。
* （Reverse）Cuthill–McKee算法

伪代码：

```
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // store all nodes which are waiting to be processed
    Set<Node> used;     // store all the used nodes
    int step = 0;       // number of steps neeeded from root to current node
    // initialize
    add root to queue;
    add root to used;
    // BFS
    while (queue is not empty) {
        step = step + 1;
        // iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                if (next is not in used) {
                    add next to queue;
                    add next to used;
                }
            }
            remove the first node from queue;
        }
    }
    return -1;          // there is no path from root to target
}
```



