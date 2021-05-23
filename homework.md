# 第一周作业

移动0

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int zero_pos = 0;
        for(int i = 0; i < nums.size(); i++)
        {
            if(nums[i] != 0)
            {
                swap(nums[zero_pos],nums[i]);
                zero_pos ++;
            }
        }
    }
};
```

2.合并两个有序链表

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == nullptr && l2 != nullptr)
        {
            return l2;
        }
        else if(l2 == nullptr && l1 != nullptr)
        {
            return l1;
        }
        else if(l1 == nullptr && l2 == nullptr)
        {
            return nullptr;
        }
        else{
            ListNode* newHead = new ListNode;
            ListNode* p1, *p2, *tail;
            if (l1->val < l2->val)
            {
                newHead->next = l1;
                p1 = l1->next;
                p2 = l2;
                tail = l1;
            }
            else 
            {
                 newHead->next = l2;
                 p2 = l2->next;
                 p1 = l1;
                 tail = l2;
            }
            while(p1 != nullptr && p2 != nullptr)
            {
                if(p1->val < p2->val)
                {
                    tail->next = p1;
                    p1 = p1->next;
                }
                else{
                    tail->next = p2;
                    p2 = p2->next;
                }
                tail = tail->next;
            }
            if(p1 != nullptr)
            {
                tail->next = p1;
            }
            else if(p2 != nullptr)
            {
                tail->next = p2;
            }
            return newHead->next;
        }
    }

};
```



# 第二周作业

二叉树的中序遍历

```c++
vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> St;
        vector<int> v;
        TreeNode* rt = root;
        while(rt || St.size()){
            while(rt){
                St.push(rt->right);
                v.push_back(rt->val);
                rt=rt->left;
            }
            rt=St.top();St.pop();
        }
        return v;        
    }

```

丑数

```c++

    int nthUglyNumber(int n) {
        int two = 0, three = 0, five = 0;
        vector<int> dp(n);
        dp[0] = 1; // dp 初始化

        for (int i = 1; i < n; ++i) {
            int t1 = dp[two] * 2, t2 = dp[three] * 3, t3 = dp[five] * 5;
            dp[i] = min(min(t1, t2), t3);

            if (dp[i] == t1) {++ two;}
            if (dp[i] == t2) {++ three;}
            if (dp[i] == t3) {++ five;}
        }

        return dp[n - 1];
    }


```

# 第三周作业

力扣46 全排列

```c++
vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> tmpRes;
        backtracing(res, tmpRes, nums, 0);
        return res;
    }
    void backtracing(vector<vector<int>>& res, vector<int>& tmpRes, vector<int>& nums, int index)
    {
        if(index == nums.size()) //index表示当前排列到第几个数了，比如给定的数组是3个数[1,2,3],当前正在进行排列的一个数组是[1,3],那么index就是1(index从0开始计数)
        {
            res.push_back(tmpRes);
            return;
        }
        for(int i = 0; i < nums.size(); i++)
        {
            //如果nums[i]已经存在于当前正在排列的数组tmpRes中，就跳过后面的执行步骤，否则，将nums[i]加入tmpRes,然后接着进行递归
            if(find(tmpRes.cbegin(), tmpRes.cend(), nums[i]) != tmpRes.end())
            {
                continue;
            }
            tmpRes.push_back(nums[i]);
            backtracing(res, tmpRes, nums, index+1);
            tmpRes.pop_back(); //tmpRes中加入了nums[i]，在这里要做回溯，然后才能进行下一次递归
        }
    }
```

 

力扣77 组合

```c++
vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> tmpRes;
        backtracing(res, tmpRes, n, k, 1); //因为是1~n中的数，所以index从1开始
        return res;
    }
    void backtracing(vector<vector<int>>& res, vector<int>& tmpRes, int n, int k, int index)
    {
        if(tmpRes.size() == k)
        {
            res.push_back(tmpRes);
            return;
        }
        //组合与排列不同的是，组合里的元素是不讲究顺序的，所以这里的i从index开始而不是从0开始
        for(int i = index; i <= n; i++) 
        {
            tmpRes.push_back(i);
            backtracing(res, tmpRes, n, k, i+1);
            tmpRes.pop_back();
        }
    }
```

