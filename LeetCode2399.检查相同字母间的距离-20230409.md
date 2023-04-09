## LeetCode刷题2399.检查相同字母间的距离

![image-20230409205911828](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304092059935.png)

![image-20230409205928280](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304092059317.png)

### **算法思想：枚举**

直接枚举所有相同的字符对 $(s[i],s[j])$ , 且满足 $(s[i] = s[j]),i<j$  , 此时两个字符之间的字母数量为 $j - i - 1$ , 然后检测该字符的匀整性。

如果字符 $s[i]$  在字符集中的顺序为 $idx$ , 这样只需要判断 $j-i-1$  是否等于 $distance[idx]$  即可。 

```C++
class Solution {
public:
    bool checkDistances(string s, vector<int>& distance) {
        int n = s.size();
        for (int i = 0; i < n; ++i)
        {
            for (int j = i + 1; j < n; ++j)
            {
                if (s[i] == s[j] && distance[s[i] - 'a'] != j - i - 1){
                    return false;
                } 
            }
        }
        return true;
    }
};
```

### 复杂度分析

时间复杂度： $O(n^2)$ , 枚举所有可能相等的字符对，一共有 $n^2$ 对不同的字符对。

空间复杂度： $O(1)$