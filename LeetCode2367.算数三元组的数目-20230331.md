## LeetCode刷题2367.算术三元组的数目

![image-20230331235625685](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202303312356007.png)

![image-20230331235647624](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202303312356660.png)



### 法一：暴力枚举

三重循环暴力枚举数组中的每个三元组，判断每个三元组是否为算数三元组，枚举结束后即可得到算数三元组的数目。

```C++
class Solution {
public:
    int arithmeticTriplets(vector<int>& nums, int diff) {
        int ans = 0;
        int n = nums.size();
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                if (nums[j] - nums[i] != diff)
                {
                    continue;
                }
                for (int k = j + 1; k < n; k++)
                {
                    if (nums[k] - nums[j] == diff)
                    {
                        ans++;
                    }
                }
            }
        }
        return ans;
    }
};
```

**时间复杂度：**
$$
O(n^3) \quad n为数组nums的长度。
$$


**空间复杂度：**
$$
O(1) \quad 不需要另外开辟存储空间
$$

### 法二：哈希集合

因为给定的数组$nums$是严格递增的，因此数组中不存在重复元素，即不存在两个相同的算数三元组。

对于数组中某个元素$x$，如果$x + diff$ 和 $x + 2 \times diff$ 也在数组中，则存在一个算数三元组。

so. 问题就从**计算$nums$有多少算数三元组** 变成了 **计算数组$nums$中有多少个元素可以做为上述的x**

为了快速判断一个元素是否在数组中，可以使用哈希集合存储数组中的所有元素，然后判断元素是否在哈希集合中。数组中所有元素加入哈希集合后, 遍历数组统计$x$的**个数**。【满足 $x + diff$ 和 $x + 2 \times diff$  都在哈希集合中】

具体思路如下：

1. 使用一个无序集合unordered_set来存储数组中的每个元素。
2. 对于每个元素$x$，判断$x + diff$和$x + 2 \times diff$是否都存在于集合中，如果是，则说明存在一个符合要求的三元组。
3. 统计符合要求的三元组数量，最后返回结果。



```C++
class Solution {
public:
    int arithmeticTriplets(vector<int>& nums, int diff) {
        unordered_set<int> hashSet;
        for(int x : nums)
        {
            hashSet.emplace(x);
        }
        int ans = 0;
        for (int x : nums) {
            if (hashSet.count(x + diff) && hashSet.count(x + 2 * diff)) {
                ans++;
            }
        }
        return ans;
    }
};
```

**时间复杂度：**
$$
O(n) \quad n为数组nums的长度。
$$

其中要遍历数组需要$O(n)$，每次将元素加入哈希集合与判断元素是否在哈希集合中的时间都是 $O(1)$。

**空间复杂度：**
$$
O(n) \quad n为数组nums的长度
$$


哈希集合需要$O(n)$的空间



### 法三：三指针

本来想自己推，推到一半，太困了，先放掉。





