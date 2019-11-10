##  3-8 在滑动窗口中做记录 Longest Substring Without Repeating Characters



### LeetCode 3

在一个字符串中寻找没有重复字母的最长子串

——如"abcabcbb"，则结果为"abc"

——如“bbbbb"，则结果为”b“

——如”pwwkew"，则结果为"wke"

#### 解题步骤

`s[i...j]`构成了一个滑动窗口

![图1](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC3%E7%AB%A0%20%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E9%97%AE%E9%A2%98%E5%85%B6%E5%AE%9E%E6%9C%80%E5%B8%B8%E8%A7%81/pic/3-8_01.png)

如果`j+1`所指的字符，在当前这个子字符串中不存在(没有重复的元素)，则`j`向前滑动，并把其所指字符纳入子字符串中

![图2](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC3%E7%AB%A0%20%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E9%97%AE%E9%A2%98%E5%85%B6%E5%AE%9E%E6%9C%80%E5%B8%B8%E8%A7%81/pic/3-8_02.png)

直到`j+1`遇到一个字符，是在子字符串中出现过的重复字符。此时`j`停止滑动，记录下当前的长度，更新结果

![图3](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC3%E7%AB%A0%20%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E9%97%AE%E9%A2%98%E5%85%B6%E5%AE%9E%E6%9C%80%E5%B8%B8%E8%A7%81/pic/3-8_03.png)

此时`i`，向前滑动直到窗口内，没有重复的字符。此时，`j`又可以继续向前滑动

![图4](https://raw.githubusercontent.com/alstonzero/Playing-Leetcode/master/%E7%8E%A9%E8%BD%AC%E7%AE%97%E6%B3%95%E9%9D%A2%E8%AF%95/%E7%AC%AC3%E7%AB%A0%20%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E9%97%AE%E9%A2%98%E5%85%B6%E5%AE%9E%E6%9C%80%E5%B8%B8%E8%A7%81/pic/3-8_04.png)



#### 代码实现。

借助了visited来判断是否有重复的字符串

```python
def lengthOfLongestSubstring(s):
    if not s: 
        return 0
    
    i,j = 0,-1
    s = list(s)
    visited = []
    res = 1  #字符串不为空时，至少有1个
    while i<len(s):
        if j+1<len(s) and s[j+1] not in visited:
            j+=1
            visited.append(s[j])
        else: #在visited有这个元素
            visited.pop(0) #删除左边元素
            i +=1
        
        #结果的保存和更新
        if len(visited)>1:
           # res = max(res,len(visited))
            res = max(res,j-i+1)
    
    return res
```



