## LeetCode刷题1041.困于环中的机器人

![image-20230411134850231](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304122250918.png)

![image-20230411134906906](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304122250924.png)

### 算法思想  **模拟**

当机器人执行完一串指令  $instructions$  后

1. 如果它的位置仍位于原点，那么不管此时它的方向是什么，机器人将陷入循环中.  $eg. GGLLGG$
2. 如果它的位置不在原点，那么需要考虑它指向的方向：
   1. 如果机器人仍然朝北，那么机器人可以不会陷入循环。假设执行完一串指令后，机器人的位置是 $(x,y)$ 且不为原点，方向依然朝北，那么执行完第二串指令后，机器人的位置便成为 $(2x,2y)$ ,会不停地往外部移动，不会陷入循环.  $eg. GG$
   2. 如果机器朝南，那么执行第二串指令时，机器人的为一会与第一次第一次相反，即第二次的位移是 $(-x, -y)$  并且结束后会回到原来的方向。这样一来，每两串指令之后，机器人都会回到原点，并且方向朝北，机器人会陷入循环。 $eg. GGLL$
   3. 如果机器人朝东，即右转了 90°。这样一来，每执行一串指令，机器人都会右转 90°。那么第一次和第三次指令的方向是相反的，第二次和第四次指令的方向是相反的，位移之和也为 0，这样一来，每四次指令之后，机器人都会回到原点，并且方向朝北，机器人会陷入循环。如果机器人朝西，也是一样的结果。 $朝东:eg. GR$   $朝西: eg.GL$

所以，想要摆脱循环，需要执行完一串指令后机器人的状态，必须是不位于原点且方向朝北。即达成 $false$ 的条件  `direction = 0 && (x != 0 && y != 0)`

则对立事件，即达成 $true$ 的条件 `direction != 0 || (x == 0 && y == 0) `

```C++
class Solution {
public:
    bool isRobotBounded(string instructions) {
        vector<vector<int>> direction = {{0,1}, {1,0}, {0,-1}, {-1,0}};//向北移动一步 向东移动一步 向南移动一步 向西移动一步
        int direcIndex = 0;//设置dircIndex=0为朝北方向
        int x = 0, y = 0;//起点位置
        for(char instruction: instructions)
        {
            if(instruction == 'G')
            {
                x += direction[direcIndex][0];
                y += direction[direcIndex][1];
            }
            else if(instruction == 'L')
            {
                direcIndex += 3;
                direcIndex %= 4;
            }
            else
            {
                direcIndex++;
                direcIndex %= 4;
            }
        }
        return direcIndex != 0 || (x == 0 && y == 0); //false:不会陷入循环 true:会陷入循环
    }
};
```

### 复杂度分析

时间复杂度:    $O(n)$  ,   $n是instructions的长度，需要遍历instructions一次$

空间复杂度:    $O(1)$  