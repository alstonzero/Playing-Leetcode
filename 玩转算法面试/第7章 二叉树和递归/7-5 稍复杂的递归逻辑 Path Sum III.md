## 7-5 稍复杂的递归逻辑 Path Sum III

### LeetCode 437

给出一棵二叉树以及一个数字sum，判断在这棵二叉树上存在多少条路径，其路径上的所有节点和为sum。

——其中路径**不一定要起始于根节点；终止于叶子节点**。

——路径可以从任意节点开始，但是只能是向下走的。

**Example:**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

**注意：**本题对于路径的要求更为宽松。

1、当前节点node不一定是路径的一部分，不能和之前的题目一样，sum-node.val

2、如果node.val在当前的路径上，此处调用一个新函数命名为fingPath（），这个函数和之前题目一样

#### 在递归算法中嵌套一个递归算法

```python
def pathSum(root,sum):
    if not root:
        return 0
    
    #以root为根节点的路径中和为sum
    res = findPath(root,sum)
    #不包含当前叶子节点的路径
    res + = pathSum(root.left,sum)
    res + = pathSum(root.right,sum)
    
    #在以node为根节点的二叉树中，寻找包含node的路径，和为sum
    #返回这样路径个数
    def findPath(node,num):
        if not node:
            return 0
        
        res = 0
        if node.val == num: #如果当前node值为num，则直接找到一个结果
            res+=1
        #递归调用，在以node为根节点的左子树中寻找
        res + = findPath(node.left,num-node.val)
        res + = findPath(node.right,num-node.val)
        
        return res

    return res        
```

