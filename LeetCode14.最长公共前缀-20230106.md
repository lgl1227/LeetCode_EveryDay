## LeetCode刷题14. 最长公共前缀

**题目：**
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

**示例：**
示例 1：

输入：strs = ["flower","flow","flight"]

输出："fl"

示例 2：

输入：strs = ["dog","racecar","car"]

输出：""

解释：输入不存在公共前缀。

**解题思路1**：

**使用内置函数**zip+set

使用zip函数取出每个单词相同位置的字母，转化成集合如果字母相同集合长度为1，如果不同就可以直接返回结果啦

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        ans = ''
        for i in list(zip(*strs)):
            if len(set(i)) == 1:
                ans += i[0]
            else:
                break
        return ans

```

```
# 例子
strs = ["flower","flow","flight"]
list(zip(*strs)) = [('f', 'f', 'f'), ('l', 'l', 'l'), ('o', 'o', 'i'), ('w', 'w', 'g')]
set(('f', 'f', 'f')) = 'f'
set(('o', 'o', 'i')) = {'i','o'}
```



**解题思路2:**

**基本的纵向查找**

本身通过for循环和条件判断，无需求最小长度，但这样写起来更为简洁一下。

```python
class Solution(object):
    def longestCommonPrefix(self, strs):
        min_len = min(len(i) for i in strs)
        ret = ""
        for i in range(min_len):
            if len(set(s[i] for s in strs)) > 1:
                break
            ret += strs[0][i]
        return ret
```

```
# 例子
strs = ["flower","flow","flight"]
min_len = 4
i = 0,1,2,3
# 纵向对比s[i]
flower
flow
flight
i = 0 时，set(s[i] for s in strs)为{'f'},求len后不大于1，添加到字符串公共前缀ret内
i = 1 时，set(s[i] for s in strs)为{'l'},求len后不大于1，添加到字符串公共前缀ret内
i = 2 时，set(s[i] for s in strs)为{'i','o'},求len后大于1,跳出循环。
ret = 'fl'
```

