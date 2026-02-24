# 1. enumerate 函数

```python
nums = [2, 7, 11]

for i in range(len(nums)):
    x = nums[i]
    print(i, x)
```

等价于

```python
for i, x in enumerate(nums):
    print(i, x)
```

# 2. 字符 -> 索引映射

```python
ord('a')  # 97
ord('b')  # 98

ord('b') - ord('a') = 1
```

# 3. 字典的`get()`函数

假设有一个字典(hash)`hash = {'刘子豪':10, '帅哥':20, '天才':30}`

你想取`'仔仔'`，你知道这里没有，你想让他返回0，但是这时候他会报错，怎么解决？使用`get()`函数

使用示例如下：

```
hash.get(x, 0) 
意思是：
如果 x 在 hash 里 → 返回 hash[x]
如果 x 不在 → 返回 0
```

# 4. 双端队列使用规则

1. 创建

   ```python
   from collections import deque
   
   dq = deque()              # 空队列
   dq = deque([1,2,3])       # 初始化
   dq = deque(maxlen=3)      # 固定长度（自动弹出旧元素）
   ```

2. 两端操作

   ```
   dq.append(x)      # 右侧加入
   dq.pop()          # 右侧弹出
   
   dq.appendleft(x)  # 左侧加入
   dq.popleft()      # 左侧弹出
   ```

   



