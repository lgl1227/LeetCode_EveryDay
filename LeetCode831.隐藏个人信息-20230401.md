## LeetCode刷题831.隐藏个人信息

![image-20230402004520125](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304020045197.png)

![image-20230402004551849](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304020045907.png)

![image-20230402004607974](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304020046005.png)



**解题思路：模拟，然后正则匹配**

首先判断 $s$ 是邮箱还是电话号码。显然，如果 s 中有字符 `@`，那么它是邮箱，否则它是电话号码。

如果 $s$ 是邮箱，我们将 $s$ 的`@`之前的部分保留第一个和最后一个字符，中间用 
`"****"` 代替"，并将整个字符串转换为小写。

如果 $s$ 是电话号码，首先我们用正则表达式移除分割符，只保留  $s$ 中的所有数字。再根据数字位数判定国家代码为几位数字，进行字符串拼接即可。

- `"***-***-XXXX" `如果国家代码为 0 位数字
- `"+*-***-***-XXXX"`如果国家代码为 1 位数字
- `"+**-***-***-XXXX"`如果国家代码为 2 位数字
- `"+***-***-***-XXXX" `如果国家代码为 3 位数字

```C++
class Solution {
public:
    vector<string> country = {"", "+*-", "+**-", "+***-"};
    string maskPII(string s) {
        //先判断是不是邮箱
        int at = s.find('@');//查找是否有@字符,有则返回@在字符串中的下标，没有则返回string::nops,即-1（当然打印出的结果不是-1，而是一个很大的数值，那是因为它是无符号的）
        if (at != string::npos) {
            transform(s.begin(), s.end(), s.begin(), ::tolower);//整个字符串转为小写
            return s.substr(0, 1) + "*****" + s.substr(at - 1);
        }
        //不是邮箱，就是电话号
        s = regex_replace(s, regex("[^0-9]"), "");//正则匹配所有非0-9的字符，将之替换为空字符，也就是123-456-7890变为1234567890
        cout << s << endl;
        return country[s.size() - 10] + "***-***-" + s.substr(s.size() - 4);//重新拼接隐藏手机号个人信息
    }
};
```

**时间复杂度：** $O(n)$,，其中 $n$ 是字符串的长度。

**空间复杂度：**$O(n)$，其中 $n$ 是字符串的长度。