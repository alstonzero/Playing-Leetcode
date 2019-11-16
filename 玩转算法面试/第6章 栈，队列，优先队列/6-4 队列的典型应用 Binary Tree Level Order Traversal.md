##  6-4 队列的典型应用 Binary Tree Level Order Traversal

### 队列的基本应用——广度优先遍历

——树：层序遍历

——图：无权图的最短路径

### Leetcode 102 Binary Tree Level Order Traversal

对一个二叉树层序遍历

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```



return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

#### 用queue实现

**通过在while循环中，再添加一个循环用来遍历当前层级的节点并保存结果**

```python
def levelOrder(root):
    if not root: 
        return []
    
    queue = []
    #visited = set()
    res = [] #用来保存最后的结果
    queue.append(root)
   
    while len(queue)!=0:#只要队列不为空，一直循环（BFS核心）
        current_res =[] #保存当前层级的结果
        
        for _ in range(len(queue)): #只遍历所在层的所有节点
            node = queue.pop(0) #取出队首元素
            #if node not in visited
            current_res.append(node.val)
            #visited.add(node)
            if node.left: #如果当前节点有左孩子
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        res.append(current_res) #把当前层的结果保存到总结果中
    
    return res
        
```



**Depth First Search**



- Use a variable to track level in the tree and use simple Pre-Order traversal
- Add sub-lists to result as we move down the levels
- Time Complexity: O(N)
- Space Complexity: O(N) + O(h) for stack space

```python
class Solution(object):
    def levelOrder(self, root):
        result = []
        self.helper(root, 0, result)
        return result
    
    def helper(self, root, level, result):
        if root is None:
            return
        
        if len(result) <= level: 
            result.append([])
        result[level].append(root.val)
        self.helper(root.left, level+1, result)
        self.helper(root.right, level+1, result)
```



### Leetcode103Binary Tree Zigzag Level Order Traversal

奇数层正常输出，偶数层颠倒输出

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:

```
[
  [3],
  [20,9],
  [15,7]
]
```

**还是层级遍历，不同的是，加入level来判断当前层级，并在添加当前层结果时，偶数层用insert添加**，把后来的元素添加到第一个。

```python
def levelOrder(root):
    if not root: 
        return []
    
    queue = []
    #visited = set()
    res = [] #用来保存最后的结果
    queue.append(root)
   
    while len(queue)!=0:#只要队列不为空，一直循环（BFS核心）
        current_res =[] #保存当前层级的结果
        
        for _ in range(len(queue)): #只遍历所在层的所有节点
            node = queue.pop(0) #取出队首元素
            #if node not in visited
            
            if level%2==1:
                current_res.append(node.val)
            else:
                current_res.insert(0,node.val)
            
            #visited.add(node)
            if node.left: #如果当前节点有左孩子
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        res.append(current_res) #把当前层的结果保存到总结果中
    
    return res

```

### Leetcode 199 Binary Tree Right Side View

![图](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-4_01.png)

[1,3,6,8,9]

**还是层级遍历，不同的是，只把每层结果最后一个元素添加到总结果中**

```python
def rightSideView(root):
    if not root: 
        return []
    
    queue = []
    #visited = set()
    res = [] #用来保存最后的结果
    queue.append(root)
   
    while queue:#只要队列不为空，一直循环（BFS核心）
        current_res =[] #保存当前层级的结果
        
        for _ in range(len(queue)): #只遍历所在层的所有节点
            node = queue.pop(0) #取出队首元素
            #if node not in visited
            current_res.append(node.val)
            #visited.add(node)
            if node.left: #如果当前节点有左孩子
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        res.append(current_res[-1]) #把当前层的结果最后一个元素保存到总结果中
    
    return res
        

```

**如果从左边看，就是把每层第一个元素添加到总结果中去**