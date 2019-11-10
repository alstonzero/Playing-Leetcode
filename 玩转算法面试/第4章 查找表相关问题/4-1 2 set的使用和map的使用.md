



## 4-1 2 set的使用和map的使用

### 两类查找问题

#### 查找有无

——元素'a'是否存在？set；集合

#### 查找对应关系（键值对应）

——元素'a'出现了几次？**map；字典dict**



### set和map

通常语言的标准库中都内置set和map

——容器类

——屏蔽了实现细节

——了解语言中标准库例常见容器类的使用

### Python中的set

`add(key)`：添加元素，可以重复添加，但不会有效果

`remove(key)`方法可以删除元素：



### Leetcode 349 Intersection of Two Arrays

给定两个数组nums，求两个数组的公共元素。

——如nums1 = [1,2,2,1]，nums2 = [2,2]

——结果为[2]。结果中每个元素只能出现一次，出现的顺序可以是任意的



```python
def intersection(nums1,nums2):
    record1 = set()
    for i in range(len(nums1)):
        record1.add(nums1[i])
    
    res = set()
    for i in range(len(nums2)):
        if nums2[i] in record1:
            res.add(nums2[i])
    return res
```



### Python中的dict（其他语言称map）

使用键-值（key-value）存储，这种key-value存储方式，在放进去的时候，必须根据key算出value的存放位置，这样，取的时候才能根据key直接拿到value。

把数据放入dict的方法，除了初始化时指定外，还可以通过key放入：

```
>>> d['Adam'] = 67
>>> d['Adam']
67
```

`in`：判断key是否存在：

```
>>> 'Thomas' in d
False
```

`get()`方法：如果key不存在，可以返回`None`，或者自己指定的value：

```
>>> d.get('Thomas')
>>> d.get('Thomas', 1)
1
```

若key存在则返回value

**还可以用来统计string字符个数**

```python
s ='aabbccdd'
d ={}
for item in s:
    d[item]=d.get(item,0)+1 
print(d)

"""
{'a': 2, 'b': 2, 'c': 2, 'd': 2}
"""
```





`pop(key)`方法：删除一个key，对应的value也会从dict中删除

```
>>> d.pop('Bob')
75
>>> d
{'Michael': 95, 'Tracy': 85}
```