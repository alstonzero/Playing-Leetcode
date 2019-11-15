## 6-1 栈的基础应用 Valid Parentheses

### 栈Stack——先进后出

#### Leetcode 20

给定一个字符串，只包含(,[,{,),],}，判定字符串中的括号匹配是否合法。

——如“()”，“()[]{}”是合法的

——如“(]","([)]"，是非法的



**入栈**

![图1](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-1_01.png)

**入栈**

![图2](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-1_02.png)

**入栈**

![图3](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-1_03.png)

**出栈，配对成功**

![图4](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-1_04.png)

**出栈，配对成功**

![图5](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-1_05.png)

**出栈，配对成功**

![图6](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-1_06.png)

**出栈，配对失败**

![图7](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC6%E7%AB%A0%20%E6%A0%88%EF%BC%8C%E9%98%9F%E5%88%97%EF%BC%8C%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97/pic/6-1_07.png)

**注意：**循环结束后，一定要判断栈是否为空。如果不为空，证明有左括号，则返回False

```python
def isValid(s):
    
    s = list(s)
    stack = []
    for i in range(len(s)):
        if s[i]=='('or s[i]=='[' or s[i]=='{': #如果s[i]为左括号，则压入栈中
            stack.append(s[i])
        
        else: #如果s[i]不为左括号
            if len(stack): #如果栈为空，证明有右括号开头，一定不配对
                return False
            
            c=stack.pop() #从栈顶取出元素
            #继续遍历s，用match存储s[i]所指的右括号相对应的左括号
            if s[i]==')':
                match = '('
            elif s[i]==']':
                match = '['
            else:
                assert s[i]=='}'#判断是否传入非法字符
                match = '{'
            #如果match的左括号与栈顶拿出的元素不相同，则一定不匹配
            if match != c:
                return False
    #当循环结束后一定要注意stack是否为空，若不为空证明stack中还存在左括号
    if len(stack)!=0:
        return False
    
    return True
            

```



### LeetCode 150.Evaluate Reverse Polish Notation





### LeetCode 71.Simplify Path

给定一个Unix系统下的路径，简化这个路径

——如 /home/，简化后为 /home

——如 /a/./b/../../c/，简化后为/c

**注意：**这个路径是否合法？不能回退的情况？多余的/