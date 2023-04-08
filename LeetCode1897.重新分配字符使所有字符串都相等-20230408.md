## LeetCode刷题1897.重新分配字符使所有字符串都相等

![image-20230408223757243](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304082238450.png)

### 算法思想

我们可以进行任意字符的移动。其实只要假设`words`的长度为 $n$  , 只需要每种字符的出现次数能够被 $n$ 整除即可，即 存在一种操作，使得操作后所有字符串均相等。

`words`每个字符串`words[i]`中都是有小写英文字母组成，所以可以定义一个 $cnt$ 数组，大小为英文字符数量 ∣Σ∣ = 26，并全部初始化为0，用两重循环来统计`words`中每种字符的出现频次。

最后，它使用 `<algorithm> `库中的` all_of `算法来检查 $cnt$ 中的每个元素是否可以被字符串总数 $n$ 整除而无余数。 如果是，则返回 $true$ ，说明可以让所有字符在所有字符串中出现的次数相等； 否则，它返回 $false$ 。



```C++
class Solution {
public:
    bool makeEqual(vector<string>& words) {
        vector<int> cnt(26, 0);//每种字符出现频次
        int n = words.size();
        for(const string & wd: words)
        {
            for(char ch: wd)
            {
                ++cnt[ch-'a'];
            }
        }
        return all_of(cnt.begin(), cnt.end(), [n](int x) {return x % n == 0;});
    }
};
```

### 复杂度分析

时间复杂度： $O(n+∣Σ∣)$ ，其中 $n$ 为 $words$ 中所有字符串的**长度总和**， $∣Σ∣ $ 为字符集的大小, 即为所有小写英文字符的数量。初始化 $cnt$ 数组的时间复杂度为 $O(∣Σ∣)$ ，遍历统计每个字符数量的时间复杂度为 $O(m)$ , 判断整除的时间复杂度为 $O(∣Σ∣)$ 。

空间复杂度： $O(∣Σ∣)$ ，即 $cnt$ 数组的大小。

### **补充1**

这两个for循环使用了范围for循环（range-based for loop）。

使用范围for循环可以简化代码的编写，尤其在遍历容器中的元素时非常方便。它的语法格式是：

```C++
for (auto element : container) {
    // ...
}
```

其中，`element` 是容器中的每个元素，`container` 可以是任何支持迭代器的容器，比如 `vector`、`list`、`set`、`map` 等。

与普通的 `for` 循环相比，范围 `for` 循环的语法更加简洁明了，并且不需要手动获取迭代器和判断迭代器是否到达容器的末尾。此外，在遍历容器时还能够防止访问越界等问题，因为范围 `for` 循环只会遍历容器中的有效元素，不会访问容器之外的区域，从而减少了出错的可能性。

### **补充2**

[参考cplusplus文档-all_of](https://cplusplus.com/reference/algorithm/all_of/?kw=all_of)

all_of返回的是bool类型，即 `true` or `false`。

```moudle
template<class InputIterator, class UnaryPredicate>
  bool all_of (InputIterator first, InputIterator last, UnaryPredicate pred)
{
  while (first!=last) {
    if (!pred(*first)) return false;
    ++first;
  }
  return true;
}
```

![image-20230408232434955](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304082324024.png)