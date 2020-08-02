## DFS

前序遍历：根结点 ---> 左子树 ---> 右子树

中序遍历：左子树---> 根结点 ---> 右子树

后序遍历：左子树 ---> 右子树 ---> 根结点

```js
// 递归版-前序遍历
let result = [];
let dfs = function (node) {
    if(node) {
        result.push(node.value);
        dfs(node.left);
        dfs(node.right);
    }
}
dfs(tree);

// 非递归
let dfs = function (nodes) {
    let result = [];
    let stack = [];
    stack.push(nodes);
    while(stack.length) {
        let node = stack.pop();
        result.push(node.value); 
        // 处理节点，比如 console.log(node.value);
        if(node.right) stack.push(node.right); // 先压入右子树
        if(node.left) stack.push(node.left); // 后压入左子树
    }
    return result;
}
dfs(tree);
```

## BFS

Breadth-first Search (BFS) 广度优先搜索，是一种盲目搜索法，目的是系统地展开并检查图中的所有节点，以找寻结果。换句话说，它并不考虑结果的可能地址，彻底地搜索整张图，直到找到结果为止。它的特点是越是接近根结点的结点将越早地遍历。

可以应用的场景：
* 查找图中所有连接组件（Connected Component）。一个连接组件是图中的最大相连子图。
* 查找连接组件中的所有节点。
* 查找非加权图中任两点的最短路径。
* 测试一图是否为二分图。
* （Reverse）Cuthill–McKee算法

在BFS中，结点的处理顺序与它们添加到队列的顺序是完全相同的顺序，即先进先出，所以广度优先搜索一般使用队列实现。

```js
// 非递归版
function bfs (node) {
    let result = [];
    let queue = [];
    queue.push(node);
    while(queue.length) {
        node = queue.shift();
        result.push(node.value); // 不要忘记访问
        // 处理节点，比如 console.log(node.value);
        node.left && queue.push(node.left);
        node.right && queue.push(node.right);
    }
    return result;
}
bfs(tree);
```



