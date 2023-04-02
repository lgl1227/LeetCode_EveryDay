## LeetCode刷题1039. 多边形三角剖分的最低得分

![image-20230402205105862](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304022051935.png)

![image-20230402205117023](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304022051075.png)

![image-20230402205126380](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304022051413.png)



有点难 **20230402-21:12**依然没有思路，看题解，理解解法，动态规划

**参考题解**

**[灵茶山艾府-视频讲解  教你一步步思考动态规划！（Python/Java/C++/Go)](https://leetcode.cn/problems/minimum-score-triangulation-of-polygon/solution/shi-pin-jiao-ni-yi-bu-bu-si-kao-dong-tai-aty6/)**

这道题可以用动态规划来解决。

首先观察题目中要求的“顶点标记的乘积”，我们可以想到使用$dp$数组保存区间$[i,j]$的最小分数。对于每个区间$[i,j]$，枚举其中的一条边$m$，将区间$[i,j]$分成两个子区间$[i,m]$和$[m,j]$，则区间$[i,j]$的得分为区间$[i,m]$的得分加上区间$[m,j]$的得分再加上三角形$[i,m,j]$的得分。由于$[i,m]$和$[m,j]$本身就是多边形，所以它们的得分已经在之前计算过了。

因此，我们可以利用状态转移方程：

$dp[i][j]=min(dp[i][j], dp[i][m]+dp[m][j]+A[i]*A[m]*A[j])$

其中$dp[i][j]$表示区间$[i,j]$的最小得分，$A[i]$表示多边形上第$i$个点的值。

需要注意的是，由于这里是多边形问题，所以我们需要枚举所有可能的三角形，也就是对于每个区间$[i,j]$，枚举其中任意一条边m。另外，当区间长度为2或3时，该区间无法分割成三角形，此时$dp[i][j]$的值为0。



```C++
class Solution {
public:
    int minScoreTriangulation(vector<int>& values) {
        int n = values.size(); // 获取多边形点的个数
        vector<vector<int>> dp(n, vector<int>(n, INT_MAX)); // 创建二维数组dp，dp[i][j]表示区间[i,j]的最小得分。初始值设为INT_MAX

        // 初始化长度为2和3的区间
        for (int i = 0; i < n - 1; i++) {
            dp[i][i + 1] = 0; // 区间长度为2，无法分割成三角形，赋值为0
        }
        for (int i = 0; i < n - 2; i++) {
            dp[i][i + 2] = values[i] * values[i + 1] * values[i + 2]; // 区间长度为3，只有一种分割方法，即(i,i+1,i+2)，赋值为对应三角形的得分
        }

        // 枚举区间长度
        for (int len = 4; len <= n; len++) {
            for (int i = 0; i <= n - len; i++) { // 枚举区间起点i
                int j = i + len - 1; // 区间终点j
                // 枚举区间内的一条边m
                for (int m = i + 1; m < j; m++) {
                    dp[i][j] = min(dp[i][j], dp[i][m] + dp[m][j] + values[i] * values[m] * values[j]); // 根据状态转移方程更新dp[i][j]的值
                }
            }
        }

        return dp[0][n-1]; // 返回多边形进行三角剖分后可以得到的最低分
    }
};

```

**解释**：本代码实现中，使用二维数组$dp$记录状态，时间复杂度为$O(n^3)$，空间复杂度为$O(n^2)$。在优化时，可以将二维数组压缩成一维数组，将状态转移过程中需要用到的$dp[i][m]$和$dp[m][j]$分别保存在两个一维数组中进行更新，即可将空间复杂度降至$O(n)$。