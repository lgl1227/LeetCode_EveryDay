## LeetCode刷题1019. 链表中的下一个更大节点

![](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/202304102059615.png)

### 算法思想：

参考题解[灵茶山艾府-【图解单调栈】两种方法，两张图秒懂！附题单（Python/Java/C++/Go）](https://leetcode.cn/problems/next-greater-node-in-linked-list/solution/tu-jie-dan-diao-zhan-liang-chong-fang-fa-v9ab/)，本题应用**单调栈**

单调栈/单调队列的题目。做题时，无论题目变成什么样，请记住一个核心原则：**及时移除无用数据，保证栈/队列的有序性**。

对于每个数，寻找它下一个更大元素

对于链表，我们可以从头节点开始递归，在「归」的过程中，就相当于是从右到左遍历链表了。

```C++
class Solution {
    vector<int> ans;
    stack<int> st;//单调栈，节点值

    void f(ListNode *node, int i){
        if(node == nullptr){
            ans.resize(i); //i为链表长度
            return;
        }
        f(node->next, i + 1);//递归
        
        while(!st.empty() && st.top() <= node->val){
            st.pop();//弹出无用数据
        }
        if(!st.empty())
            ans[i] = st.top();//栈顶就是第i个节点的下一个更大元素 

        st.push(node->val);//归的过程即为从右向左遍历,入栈
    }    
public:
    vector<int> nextLargerNodes(ListNode* head) {
        f(head, 0);
        return ans;
    }
};
```

非递归，可以先反转链表

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
    //反转链表
    ListNode *reverseList(ListNode *head){
        ListNode *pre = nullptr, *cur = head;
        while(cur){
            ListNode *nxt = cur->next;
            cur->next = pre;
            pre = cur;
            cur = nxt;
        }
        return pre;
    }
public:
    vector<int> nextLargerNodes(ListNode* head) {
        head = reverseList(head);
        vector<int> ans;
        stack<int> st;
        for(auto cur = head; cur; cur = cur->next){//将反转后的链表从头遍历
            while(!st.empty() && st.top() <= cur->val){
                st.pop();
            }
            ans.push_back(st.empty() ? 0 : st.top());//栈顶就是第i个节点的下一个更大元素
            st.push(cur->val);
        }
        //由于是倒着记录答案的，返回前要把答案反转
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

### 复杂度分析

时间复杂度：  $O(n)$  ，其中n为链表的长度。虽然我们写了个二重循环，但站在每个元素的视角看，这个元素在二重循环中最多入栈出栈各一次，因此整个二重循环的时间复杂度为  $O(n)$ 

空间复杂度：  $O(n)$  ，单调栈中最多有  $O(n)$   个数