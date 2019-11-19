## 7-4 定义递归问题 Binary Tree Path

### Leetcode 257.Binary Tree Paths

给定一棵二叉树，返回所有表示从根节点到叶子节点路径的字符串。

——如右图所示的二叉树

——结果为["1->2->5","1->3"]

**Example:**

```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```



#### 解法：

![图1](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC7%E7%AB%A0%20%E4%BA%8C%E5%8F%89%E6%A0%91%E5%92%8C%E9%80%92%E5%BD%92/pic/7-4_01.png)



此时求解完成了以2为根节点的二叉树的所有路径的字符串

![图2](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC7%E7%AB%A0%20%E4%BA%8C%E5%8F%89%E6%A0%91%E5%92%8C%E9%80%92%E5%BD%92/pic/7-4_02.png)



同理，求解完成了以3为根节点的二叉树的路径字符串

![图3](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC7%E7%AB%A0%20%E4%BA%8C%E5%8F%89%E6%A0%91%E5%92%8C%E9%80%92%E5%BD%92/pic/7-4_03.png)



最后再把左子树和右子树的结果返回根节点，得到根节点的所有路径字符串



![图4](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC7%E7%AB%A0%20%E4%BA%8C%E5%8F%89%E6%A0%91%E5%92%8C%E9%80%92%E5%BD%92/pic/7-4_04.png)

**代码实例**

定义递归出口：1、root为空时；2、当前节点为叶子节点时

```python
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        res = []
        if not root:
            return res
        if not root.left and not root.right:
            res.append(str(root.val))
        
        #左子树的结果
        resleft = binaryTreePaths(root.left)
        for item in resleft:
              temp = str(root.val)+"->"+str(item)
              res.append(temp)
        
        resright = binaryTreePaths(root.right)
        for item in resright:
            temp2 = str(root.val)+"->"+str(item)
            res.append(temp2)
            
        return res
        
```



### Leetcode 113. Path Sum2

给定一个二叉树，返回所有从根节点到叶子节点的路径，其和为sum。

**Example:**

Given the below binary tree and `sum = 22`,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```

Return:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```





```python


```



### Leetcode 129.Sum Root to Leaf Numbers

给定一棵二叉树，每个节点只包含数字0-9，从根节点到叶子节点的每条路径可以表示成一个数，求这些树的和。

**Example:**

```
Input: [1,2,3]
    1
   / \
  2   3
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

**Example 2:**

```
Input: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```