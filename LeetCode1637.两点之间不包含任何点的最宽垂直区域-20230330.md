## LeetCode刷题1637. 两点之间不包含任何点的最宽垂直区域

![image-20230330220737089](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202303302207151.png)

![](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202303302210501.png)

**思路**：数组  排序  

啧，这个题直接别被它的难度唬住了，思考一下其实很简单，就是将点排序后，全部投影到x轴，求相邻的两个点的最大距离。

```C++
class Solution {
public:
    int maxWidthOfVerticalArea(vector<vector<int>>& points) {
        sort(points.begin(), points.end());
        int mx = 0;
        for (int i = 0; i < points.size() - 1; ++i)
        {
            mx = max(points[i+1][0] - points[i][0], mx);
        }
        return mx;
    }
};
```

**复杂度分析**

**时间复杂度：**
$$
O(n\ log\ n),\ 其中 n 是输入数组的长度，排序消耗 O(n\ log\ n) 时间复杂度。
$$
**空间复杂度：**
$$
O(log\ n),\ 为排序的空间复杂度
$$
