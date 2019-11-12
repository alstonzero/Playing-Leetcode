## 4-3 set和map不同底层实现的区别

### [python]list, tuple, dictionary, set的底层细节

https://blog.csdn.net/siyue0211/article/details/80560783

### Python中dict的实现细节

CPython使用伪随机探测(pseudo-random probing)的**散列表(hash table)**作为字典的底层数据结构。由于这个实现细节，只有**可哈希**的对象才能作为字典的键。

**Python中所有不可变的内置类型都是可哈希的。可变类型（如列表，字典和集合）就是不可哈希的，因此不能作为字典的键。**

字典的三个基本操作（添加元素，获取元素和删除元素）的平均事件复杂度为O(1)，但是他们的平摊最坏情况复杂度要高得多，为O(N).

操作	平均复杂度	平摊最坏情况复杂度
获取元素	O(1)	O(n)
修改元素	O(1)	O(n)
删除元素	O(1)	O(n)
复制	O(n)	O(n)
遍历	O(n)	O(n)
还有一点很重要，在复制和遍历字典的操作中，最坏的复杂度中的n是字典曾经达到的最大元素数目，而不是当前的元素数目。换句话说，如果一个字典曾经元素个数很多，后来又大大减小了，那么遍历这个字典可能会花费相当长的事件。因此在某些情况下，如果需要频繁的遍历某个词典，那么最好创建一个新的字典对象，而不是仅在旧字典中删除元素。



### Python中set的实现



### 练习题



### Leetcode242 Valid Anagram

https://leetcode.com/problems/valid-anagram/

判断字符串t是否是字符串s变换字符顺序后得到的结果

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

#### 解题：

创建两个dict分别记录s和t的字符和该字符出现的频率，再比较两个记录的dict是否相等。

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        record = {}
        record2 = {}
        for i in range(len(s)):
            record[s[i]] = record.get(s[i],0)+1
            
        for i in range(len(t)):
            record2[t[i]] = record2.get(t[i],0)+1
            
        return record2 == record
        
```

### Leetcode202 Happy Number

https://leetcode.com/problems/happy-number/

一个数将其替换为其各位数字的平方和，重复这个过程，如果最终能得到1，这是happy number，如果这个过程陷入了一个不包含1的循环，则不是happy number

**Example:** 

```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

#### 解题：

用set()记录每次操作的num，如果该num没有在set中出现，则才能进行循环操作；

```python
def happyNumber(num):
    record = set()
    
    while num not in record:#如果num不在set中进行循环操作；若在set中证明进入死循环，不符合题目要求
        record.add(num) #记录每次操作的num
        squareSum = 0 #每次的和是要重新计算的
       
        #把一个数字的所有位数取出，并进行操作
        while num>0: 
            remain = num%10
            squareSum += remain*remain
            num = num//10
        
        
        if squareSum ==1:
            return True
        else:
            num = squareSum
    
    return False
```



### Leetcode290 Word Pattern

https://leetcode.com/problems/word-pattern/

给出一个模式(pattern)以及一个字符串，判断这个字符串是否符合模式？

**Example 1:**

```
Input: pattern = "abba", str = "dog cat cat dog"
Output: true
```

**Example 2:**

```
Input:pattern = "abba", str = "dog cat cat fish"
Output: false
```

**Example 3:**

```
Input: pattern = "aaaa", str = "dog cat cat dog"
Output: false
```

**Example 4:**

```
Input: pattern = "abba", str = "dog dog dog dog"
Output: false
```

**注意：**字符集？ 空串符合任意模式？还是不符合任意模式？

#### 解题

```python
def wordPattern(pattern, word_str):

        words = word_str.split(" ")
        if len(pattern) != len(words):
            return False

        pattern_map, word_map = {}, {}
        for i in range(len(pattern)):
            if pattern_map.get(pattern[i], -1) != word_map.get(words[i],-1):
                return False
            pattern_map[pattern[i]] = pattern_map.get(pattern[i], 0)+i
            word_map[words[i]] = word_map.get(words[i],0)+i

        return True

```

### Leetcode205.Isomorphic Strings





### Leetcode451 Sort Characters By Frequency

