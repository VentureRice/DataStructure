# Binary Tree


### 定义一个二叉树

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
```

### 二叉树的中序遍历(94)

```python
def inorderTraversal(self, root: TreeNode):
    if not root:
        return []
    return inorderTraversal(root.left)+[root.val]+inorderTraversal(root.right)
```

### 二叉树的前序遍历(144)

```python
def preorderTraversal(self, root: TreeNode):
    if not root:
        return []
    return [root.val]+self.preorderTraversal(root.left)+self.preorderTraversal(root.right)
```

### 二叉树的后序遍历(145)

```python
def postorderTraversal(self, root: TreeNode):
    if not root:
        return []
    return postorderTraversal(root.left)+postorderTraversal(root.right)+[root.val]
```

### 二叉树的层序遍历(102)


BFS模版

```python
def levelOrder(root: TreeNode):
    queue = [root]
    res = []
    while queue:
        size = len(queue)
        level = []
        for _ in range(size):
            cur = queue.pop(0)
            if not cur:
                continue
            level.append(cur.val)
            queue.append(cur.left)
            queue.append(cur.right)
        if level:
            res.append(level)
    return res

```

### 二叉树的所有路径


二叉树的深度优先搜索

```python
class Solution:
    def binaryTreePaths(self, root):
        """
        :type root: TreeNode
        :rtype: List[str]
        """
        def construct_paths(root, path):
            if root:
                path += str(root.val)
                if not root.left and not root.right:  # 当前节点是叶子节点
                    paths.append(path)  # 把路径加入到答案中
                else:
                    path += '->'  # 当前节点不是叶子节点，继续递归遍历
                    construct_paths(root.left, path)
                    construct_paths(root.right, path)

        paths = []
        construct_paths(root, '')
        return paths
```

### N叉树的前序遍历（589）


给定一个 N 叉树，返回其节点值的前序遍历。

```python
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
```

```python
node = Node(1,[Node(3,[Node(5),Node(6)]),Node(2),Node(4)])
```

```python
# DFS
if not node:
    ptint(node)
visited = [node]
order = []

while visited:
    cur_node = visited.pop()
    if cur_node.children:
        visited.extend(cur_node.children[::-1])
    order.append(cur_node.val)
    
print(order)
```

```python

```
