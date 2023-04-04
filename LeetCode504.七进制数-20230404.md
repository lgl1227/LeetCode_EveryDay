## LeetCode刷题504.七进制数

![image-20230404231615984](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304042316046.png)

### **解题思路**

e.. 简单题 输入肯定是一个十进制的整数 （可正可负），将其转化为七进制

**知识点：十进制整数转任意进制 除留取余 高位->低位 **

十进制int类型转七进制字符串,使用不断整除的方法加到字符串末尾，最后反转。注意考虑负号。

1. 对0和负数进行特判，负数单独处理符号后 统一 变成正整数转换为七进制数
2. num对7取模，并将结果添加到字符串ans末尾，再num=num/7，重复此操作，直到num=0
3. 反转字符串ans 使用reverse(ans.begin(),ans.end());



```c++
class Solution {
public:
    string convertToBase7(int num) {
        string zero = "0";
        string ans = "";
        if(num == 0)//num为0
            return zero;

        bool pos = num >= 0 ? true:false;//布尔值记录num是正整数还是负整数

        if(!pos)//num是负数，将其转为相反数计算7进制结果再添符负号
            num = -num;
        while(num > 0)//num为正整数时
        {
            ans += num % 7 + '0';//每次加单引号零 保证添加的是字符，也可用强制类型转换to_string(num % 7)
            num /= 7;
        }
        if(!pos)//因为num是负数
            ans += "-";//添负号
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

### **复杂度分析**

**时间复杂度：**$O(log_7 \ n)$ 等价于$O(log \ n)$

**空间复杂度：**$O(log_7 \ n)$ 等价于$O(log \ n)$