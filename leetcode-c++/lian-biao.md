# 链表

```
//Definition for singly-linked list.
    struct ListNode {
      int val;
      ListNode *next;
      ListNode() : val(0), next(nullptr) {}
      ListNode(int x) : val(x), next(nullptr) {}
      ListNode(int x, ListNode *next) : val(x), next(next) {}
    };
```

### [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

解法一：

```

//将A放入set，然后遍历B，对于遍历到的每个节点，判断该节点是否在set中。
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> visited;
        ListNode *temp = headA;
        while (temp != nullptr) {
            visited.insert(temp);
            temp = temp->next;
        }
        temp = headB;
        while (temp != nullptr) {
            if (visited.count(temp)) {
                return temp;
            }
            temp = temp->next;
        }
        return nullptr;
    }
};
```

1.set 容器中不允许有重复元素出现 set插入时自动排序

3.multiset 允许容器中有重复元素出现

4.unordered\_set 无序

.insert() 插入 .erase()删除

.find(key) 查找key是否存在 返回找到元素的的是迭代器 ，若不存在，返回set.end() .count(key) 统计key的元素个数

解法二：

```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (headA == nullptr || headB == nullptr) {
            return nullptr;
        }
        ListNode *pA = headA, *pB = headB;
        while (pA != pB) {
            pA = pA == nullptr ? headB : pA->next;
            pB = pB == nullptr ? headA : pB->next;
        }
        return pA;
    }
};
```

设 A 的长度为 a + c，B 的长度为 b + c，其中 c 为尾部公共部分长度，可知 a + c + b = b + c + a。

当访问 A 链表的指针访问到链表尾部时，令它从链表 B 的头部开始访问链表 B；同样地，当访问 B 链表的指针访问到链表尾部时，令它从链表 A 的头部开始访问链表 A。这样就能控制访问 A 和 B 两个链表的指针能同时访问到交点。

### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

解法一：

```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
       ListNode *prev = nullptr;
       ListNode *p = head;
       while(p != nullptr){
           ListNode *q = p->next;	//临时变量
           p->next = prev;
           prev = p;
           p = q;
       }
       return prev;
    }
};
```

![迭代.gif](https://cdn.jsdelivr.net/gh/YZJss/tuchuang@main/7d8712af4fbb870537607b1dd95d66c248eb178db4319919c32d9304ee85b602-%E8%BF%AD%E4%BB%A3.gif)

解法二： 递归

```
```

### [21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

解法一：

```
class Solution {
    public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode *dummy = new ListNode();	//dummy指针
        ListNode *p = dummy;
        while(l1 != nullptr && l2 != nullptr){
            if(l1->val > l2->val){
                p->next = l2;
                l2 = l2->next;
            }
            else{
                p->next = l1;
                l1 = l1->next;
            }
            p = p->next;
        }
        if(l1 == nullptr){
            p->next = l2;
        }
        else{
            p->next = l1;
        }
        return dummy->next;
    }
};
```

解法二： 递归

```
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == NULL) {
            return l2;
        }
        if (l2 == NULL) {
            return l1;
        }
        if (l1->val <= l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        }
        else{
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```

### [83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

```
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *p = head;
        while(p != nullptr && p->next != nullptr){
            if(p->val != p->next->val){
                p = p->next;      
            }
            else{
                p->next = p->next->next;
            }
        }
        return head;
    }
};
```

### [19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

解法一：

```
class Solution {
public:
    int getLength(ListNode* head) {
        int length = 0;
        while (head) {
            length++;
            head = head->next;
        }
        return length;
    }

    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode();
        dummy->next = head;
        int length = getLength(head);
        ListNode* cur = dummy;
        for (int i = 1; i < length - n + 1; ++i) {
            cur = cur->next;
        }
        cur->next = cur->next->next;
        return dummy->next;
    }
};
```

解法二：快慢指针

```
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode();
        dummy->next = head;
        ListNode *p = dummy;
        ListNode *q = head; 
        while(n){
            q = q->next;
            n--;
        }
        while(q){
            p = p->next;
            q = q->next;
        }
        p->next = p->next->next;
        return dummy->next;
    }
};
```

### [24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

```
//三个节点
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummyHead = new ListNode();
        dummyHead->next = head;
        ListNode* temp = dummyHead;
        while (temp->next != nullptr && temp->next->next != nullptr) {
            ListNode* node1 = temp->next;
            ListNode* node2 = temp->next->next;
            temp->next = node2;
            node1->next = node2->next;
            node2->next = node1;
            temp = node1;
        }
        return dummyHead->next;
    }
};
```

### [445. 两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)

解法一：反转链表求和

```
 ListNode* fanzhuan(ListNode* head){
        ListNode *cur = head;
        ListNode *prev = nullptr;
        while(cur){
            ListNode *temp = cur->next;
            cur->next = prev;
            prev = cur;
            cur = temp;
        }
        return prev;
    }
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        l1 = fanzhuan(l1);
        l2 = fanzhuan(l2);
        ListNode *dummy = new ListNode();
        ListNode *p = dummy;

        int carry = 0;              
        while (l1 || l2)
        {
            carry += (l1 == nullptr ? 0 : l1->val) + (l2 == nullptr ? 0 : l2->val);
            p = p->next = new ListNode(carry % 10);
            carry /= 10;
            if (l1) l1 = l1->next;
            if (l2) l2 = l2->next;
        }
        if (carry) p->next = new ListNode(1);
        return fanzhuan(dummy->next);
    }
};
```

解法二：栈

```
```

### [234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

```
ListNode* mid(ListNode*head){
    ListNode* slow = head;
    ListNode* fast = head;
    while(fast->next != nullptr &&fast->next->next != nullptr){
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
ListNode* fanzhuan(ListNode* head) {
       ListNode *prev = nullptr;
       ListNode *p = head;
       while(p != nullptr){
           ListNode *q = p->next;	//临时变量
           p->next = prev;
           prev = p;
           p = q;
       }
       return prev;
}
class Solution {
public:
    bool isPalindrome(ListNode* head) {
    ListNode *dummy = head;
    ListNode *m = mid(head);
    m = fanzhuan(m->next);
    while(m != nullptr){
        if(dummy->val != m->val) return false;
        dummy = dummy->next;
        m = m->next;
    }
    return true;
    }
};
```

### [725. 分隔链表](https://leetcode-cn.com/problems/split-linked-list-in-parts/)

```
 int getlength(ListNode* head){
     int length = 0;
     while(head){
         head = head->next;
         length++;
    }
    return length;
 }
class Solution {
public:
    vector<ListNode*> splitListToParts(ListNode* head, int k) {
        int n = getlength(head);
        int quotient = n / k, remainder = n % k;
        vector<ListNode*> parts(k,nullptr);
        ListNode *curr = head;
        for (int i = 0; i < k && curr != nullptr; i++) {
            parts[i] = curr;
            int partSize = quotient + (i < remainder ? 1 : 0);
            for (int j = 1; j < partSize; j++) {
                curr = curr->next;
            }
            ListNode *next = curr->next;
            curr->next = nullptr;
            curr = next;
        }
        return parts;
    }
};
```

### [328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)

```
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if (head == nullptr) {
            return head;
        }
        ListNode* evenHead = head->next;
        ListNode* odd = head;
        ListNode* even = evenHead;
        while (even != nullptr && even->next != nullptr) {
            odd->next = even->next;
            odd = odd->next;
            even->next = odd->next;
            even = even->next;
        }
        odd->next = evenHead;
        return head;
    }
};
```

![image.png](https://cdn.jsdelivr.net/gh/YZJss/tuchuang@main/1605227711-BsDKjR-image.png)
