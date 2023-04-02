## LeetCodes刷题26.删除有序数组中的重复项

![image-20230329232102943](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202303292321012.png)

![image-20230329232124794](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202303292321840.png)



**双指针法**

**思路：**

- 由于数组已经是有序的，因此重复元素一定是连续的，我们可以使用双指针法来解决这个问题。
- 定义两个指针 i 和 j，其中 i 是慢指针，而 j 是快指针。只要 nums[i] = nums[j]，我们就增加 j 以跳过重复项。【j的自加放到循环条件】
- 当遇到 nums[j] != nums[i] 时，将 nums[j] 的值复制到 nums[i + 1] 处，然后递增 i，直到 j 到达数组的末尾为止。【i的自加放到循环体中】

**算法实现**：

```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.empty())
            return 0;
        int i = 0;
        for(int j = 1; j < nums.size(); ++j)
        {
            if(nums[j]!=nums[i])
                ++i;
                nums[i] = nums[j];
        }
        return i + 1;
    }
};
```



时间复杂度：	
$$
O(n)
$$
空间复杂度：
$$
O(1)
$$
