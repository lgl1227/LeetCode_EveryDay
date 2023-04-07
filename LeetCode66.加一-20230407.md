## LeetCode刷题66.加一

![image-20230407222047753](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304072220843.png)

### 算法思想

​	加一只需要考虑两种情况.

1. 除9之外的数字加一；
2. 数字9.

加一得十个位数为 $0$ 加法运算如不出现进位就运算结束了且进位只会是一。

所以只需要判断有没有进位并模拟进位即可

然后特殊情况如99、999之类的数字时，循环到最后也需要进位，这种取巧直接重新初始化一个比原来长度加1的数组，然后新数组首位直接赋为1即可。

```C++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int len = digits.size();
        for(int i = len - 1; i >= 0; i--)
        {
            digits[i]++;
            digits[i] = digits[i] % 10;
            if(digits[i] != 0)
                return digits;
        }
        //如果是99 或者 999 等情况
        digits = vector<int>(len + 1);//直接重新初始化比原来长度多1的int数组 ps: 默认就是全0的
        digits[0] = 1;//新的digits数组首位为1
        return digits;
    }
};
```

### **详细过程**

```eg.
digits = [1,2,3]
len = 3
i=2时  
digits[2]++ //[1,2,4]
digits[2]%10 = 4
直接 return digits = [1,2,4]


digits = [1,2,9]
len = 3
i=2时
digits[2]++ //[1,2,0]
digits[2] = 0%10 = 0
继续循环，i=1
digits[1]++ //[1,3,0]
digits[1] = 3%10 = 3
return digits = [1,3,0]


digits = [9,9,9]
len = 3
i=2时
digits[2]++ //[9,9,0]
digits[2] = 0%10 = 0
i=1时
digits[1]++ //[9,0,0]
digits[1] = 0%10 = 0
i=0时
digits[0]++ //[0,0,0]
digits[0] = 0%10 = 0

新的digits = vector<int> (len+1) // [0,0,0,0]
digits[0] = 1
return digits = [1,0,0,0]

```

### **复杂度分析**

时间复杂度：  $O(n)$

空间复杂度： $O(1)$