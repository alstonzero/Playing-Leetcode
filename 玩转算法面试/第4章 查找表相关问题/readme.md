## Python中的dict（其他语言称map）

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
### Python中的set
**与dict不同之处：没有value**

`add(key)`：添加元素，可以重复添加，但不会有效果

`remove(key)`方法可以删除元素：
