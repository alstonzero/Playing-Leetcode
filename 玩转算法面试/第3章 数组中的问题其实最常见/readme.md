## 滑动窗口代码模板
在数组arr中，arr[i...j]为滑动窗口

```python
i,j = 0,-1  #初始时，窗口中不能有元素，右边界为-1
"""
result 初始值
辅助变量等
"""

while i<len(arr): #只要窗口左边不越界，就能一直滑动下去
    
    if j+1<len(arr) and condition: #只要窗口右边界不越界，且满足题目条件时进行操作
        j+=1 
        process(arr[j])
    
    else:  #当前窗口不满足题目条件时，先进行操作，再使左边界向前滑动
        process(arr[i]) 
        i-=1
"""
    记录，并更新result
"""

return result
```

