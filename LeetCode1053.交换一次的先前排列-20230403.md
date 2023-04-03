## LeetCode刷题1053.交换一次的先前排列

![image-20230403211555815](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304032115880.png)



### **题目解析：**

大致的意思是  

交换数字$arr[i]$和$arr[j]$的位置后得到的数组 组成的数字  $<$	原先数组组成的数字 并且 在所有可能的排序中又是最大的。

### **解题思路：**

贪心思想：为了让交换后所构成的数组最大化，需要`保证交换的两个数发生在低位`

- -> 从后往前遍历， 指针$left$指向数组倒数第二位元素，**也就是数组下标$arr[n-2]$**,为的是和后一位元素$left+1$【**也就是数组下标$arr[n-2+1]$**】进行比较，如果后一位大，说明 交换这两个位置只会让数组组成的数字更大，**显而易见，只有当后一位小的时候，我们就进行交换**

- -> 这样构成了自左向右单调递增的性质，因此当后一位元素比前一位元素小的时候， 指针$right$指向数组最后一位元素，也就是数组下标$arr[n-1]$，从后往前遍历，交换$arr[left]$ 和 $arr[right]$。即为最终答案

- **->注：**若数组中存在重复元素，只有取重复元素对应元素下标最小时，组成的数字值才是最大的
  1. **case1:**(如重复值在末尾93777 -> 73977才是最大的) $arr[right] == arr[right-1]$
  2. **case2:**(如重复值在中间3113 -> 1313)$arr[right] >= arr[left]$

```C++
class Solution {
public:
    vector<int> prevPermOpt1(vector<int>& arr) {
        int n = arr.size();//数组长度
        int right = n-1;
        for(int left = n-2; left >= 0; left--)
        {
            //前一位比后一位大
            if(arr[left] > arr[left+1])
            {
                //存在重复元素，计算到数组元素下标最小的
                while(arr[right] == arr[right-1] || arr[right] >= arr[left])
                {
                    right--;
                }
                swap(arr[left], arr[right]);
                break;
            }
        }
        return arr;
    }
};
```



### **复杂度分析:**

**时间复杂度：**$O(n)$

**空间复杂度：**$O(1) \quad返回值不计入空间复杂度。$

