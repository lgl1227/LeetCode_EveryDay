## LeetCode刷题104.二叉树的最大深度

![image-20230327220607752](https://blog-1304436410.cos.ap-beijing.myqcloud.com/leetcode/image-20230327220607752.png)

没什么好说的，二叉树的四种遍历方法，先序、中序、后序、层次遍历。使用层次遍历(BFS)求二叉树的最大深度。

- 1.首先我们from collections import deque，创建一个双端队列
- 2.然后我们把二叉树的root加进这个队列里面
- 3.然后我们开始循环,每一次循环都是遍历二叉树的一层结点，从头结点开始，每个结点我们都要判断其是否有左右子树，有就加进队列里，没有就跳过，然后每一次循环都要给深度+1
- 4.循环结束，return depth即可

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == nullptr)
            return 0;
        int depth = 0;
        queue<TreeNode*> q;//定义队列
        q.push(root);//根节点入队
        while(!q.empty())
        {
            int size = q.size();
            for(int i = 0; i < size;i++)
            {
                TreeNode* node = q.front();
                q.pop();//队头元素出队
                if(node->left != nullptr)
                    q.push(node->left);
                if(node->right != nullptr)
                    q.push(node->right);
            }
            ++depth;
        }
        return depth;
    }
};
```

