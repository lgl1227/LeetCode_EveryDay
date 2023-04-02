## LeetCode刷题415.字符串相加

![image-20230328222548862](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202303282225912.png)

**解题思路：**

本题可以使用模拟的方法，从最低位开始逐位相加，同时记录进位的值，最后将结果翻转输出即可。

时间复杂度：
$$
O(max(N,M))，其中 N 和 M 分别为 num1 和 num2 的长度。
$$
空间复杂度：
$$
O(max(N,M))，即为存储答案所需的空间。
$$
注：本题还有其他解法，例如：高精度加法、字符串加法等，感兴趣的读者可以自行探索。

<span style="color:red">补充：</span>

```
ans.push_back(sum % 10 + '0')

AI：这行代码的意思是将当前计算出的余数（即sum % 10）转换为字符类型，并将其加入到名为ans的字符型向量的末尾。'0'是ASCII码中数字0的字符表示，加上一个数字的ASCII码值即可得到对应的字符。

C++ push_back是vector自带的吗？

AI：是的，push_back是vector类的成员函数之一，用于在vector的末尾添加一个元素。

```



```C++
class Solution {
public:
    string addStrings(string num1, string num2) {
        string ans = "";//返回结果
        int carry = 0;//记录进位
        int i = num1.size() - 1, j = num2.size() - 1;
        while(i >= 0 || j >= 0 || carry != 0)
        {
            int x = i >= 0 ? num1[i] - '0':0;
            int y = j >= 0 ? num2[j] - '0':0;
            int sum = x + y + carry;
            ans.push_back(sum % 10 + '0');
            carry = sum / 10;
            i--;
            j--;
        }
        reverse(ans.begin(), ans.end());//翻转
        return ans;
    }
};
```

**话说回来，用chatgpt辅助刷题，不会的某段代码直接问它啥意思，这样刷题效率还挺高**<span style="color:red">但是，请一定要思考怎么解，自己尝试着去写一下，直接让chatgpt替你解题万万不可取。且你不指定解法的话，chatgpt似乎往往只会随机给你一种关注度高的解法</span><font color="blue">【此解法不一定效率最高、不一定难度最高】</font>