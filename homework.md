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

