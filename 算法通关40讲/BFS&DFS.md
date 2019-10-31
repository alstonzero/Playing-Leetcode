## 广度优先搜索 BFS——层层推进

### 按层遍历，逐层深入；无需递归，队列辅助

```python
def BFS(graph,start,end):
    
    queue = [] #辅助队列
    queue.append([start])
    visited.add(start)  #visited是一个集合set，把访问过的节点压入进去
    
    while queue: #只要队列中有元素
        node = queue.pop(0) #把队列头元素取出
        visited.add(node) #首先标记这个节点已被访问
        
        process(node) #进行一系列操作
        nodes = generate_related_nodes(node) #该node的相邻节点没有被访问过
        queue.push(nodes) #将node的没被访问过的相邻节点加入队列       
```



## 深度优先搜索DFS——一查到底

### 先一竿子查到底，有漏网之鱼再回溯

#### 递归写法(推荐)

```python
visited = set() #visited是一个集合set，把访问过的节点压入进去
def dfs(node,visited):
    visited.add(node) 
    #process current node here 
    #进行当前节点的操作
    ...
    
    for next_node in node.childern(): #把node相邻节点拿出来
        if not next_node in visited: #如果这个相邻节点没有被访问
            dfs(next_node,visited) #则递归进行访问
```

#### 非递归——stack栈辅助

```python
def DFS(graph,start):
    if start is None:
        return []
    
    visited = set()
    stack = []
    stack.append([start])
    
    while stack:
        node = stack.pop()
        visited.add(node)
        
        process(node) #操作当前node
        nodes = generate_related_nodes(node)
        stack.push(nodes)
```

## 例题

### 102——Binary Tree Level Order



#### 方法1：BFS，O(n),关键判断该node是否为最后一个node

a，不建议把level 信息加入到queue中

a，不建议把level 信息加入到queue中

**b，最佳方法Betch process**

关键点：1，记得BFS的模板，queue不为空时，不断处理queue中的节点。2，同时把新的一层加入queue中

```python
class Solution(object):
    def levelOrder(self,root):
        if not root: #首先判断root
            return []
        
        result = []
        queue = collections.deque() #调包双端队列
        queue.append(root)
        
        #visited = set(root) 本题是树结构，不会走回头路
        
        while queue: #BFS灵魂，只要queue不为空，一直循环
            level_size = len(queue) #先取出当前层的总长度
            current_level = [] #当前层结果
        #根据当前层的总长度，每次把queue的头元素取出    
            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val) #把当前层元素依次加入
                #如果该节点有子节点，则左右节点分别加入队列中，由于加入到队列的后面，因此在当前循环中不会被操作
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
             #当前层处理完毕后，将当前层的结果放到result中   
             result.append(current_level)
          
         return result
```



Java代码

```java
public List<List<Integer>> levelOrder(TreeNode root){
    List<List<Interger>> res = new ArrayList<>();
    if(root == null)
        return res;
    
    Queue<TreeNode> q = new LinkedList<>();
    q.add(root);
    
    while(!q.isEmpty()){
        int levelSize = q.size();
        List<Interger> currLevel = new ArrayList<>();
        
        for(int i = 0;i<levelSize;i++){
            TreeNode currNode = q.poll();
            currLevel.add(currNode.val);
            if(currNode.left != null)
                q.add(currNode.left);
            if(currNode.right != null)
                q.add(currNode.right);
        }
        res.add(currLevel);
    }
    return res;
}
```



#### 方法2：DFS（创新）



```python
class Solution(object):
    def levelOrder(self,root):
        if not root:
            return []
        self.result = []
        self._dfs(root,0)
        return self.result
    
    def _dfs(self,node,level):
        if not node:
            return
        
        if len(self.result)<level+1:
            self.result.append([])
            
        self.result[level].append(node.val)
        
        self._dfs(node.left,level+1)
        self._dfs(node.right,level+1)
        
```



### 104，111——Max/Min depth

#### 题目：二叉树的最大深度和最小深度

给定二叉树[3,9,20,null,null,15,7,null,4]返回它的最大深度4，最小深度2



```python
class Solution:
    def maxDepth(self,root):
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left),self.maxDepth(root.right))
    
    if root==null:
        return 0
    else:
        return 1+Math.max(maxDepth(root.left),self.maxDepth(root.right))
```





```java
class Solution{
    p
}
```



```python
class Solution:
    def minDepth(self,root):
        if root == null:
            return 0
        left = minDepth(root.left)
        right = minDepth(root.right)
        if left ==0 || right ==0:
            return left+right+1
        else:
            min(left,right)+1
```



### 22.Generate Parentheses

题目：括号生成

示例：给出n代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

例如，给出n=3，生成结果为：

["((()))","(()())","(())()","()(())","()()()"]



```python
class Solution(object):
    def generateParenthesis(self,n):
        self.list = []
        self._gen(0,0,n,"")
        return self.list
    
    def _gen(self,left,right,n,result):
        if left == n and right == n:
            self.list.append(result)
            return
        if left <n:
            self._gen(left+1,right,n,result+"(")
        if left>right and right <n:
            self._gen(left,right+1,n,result+")")
            
```

