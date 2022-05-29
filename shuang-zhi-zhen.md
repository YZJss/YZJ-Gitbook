# 双指针

### [167. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

```
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        for (int i = 0; i < numbers.size(); i++) {
            //二分查找算法
            int low = i + 1, high = numbers.size() - 1;
            while (low <= high) {
                int mid = (high - low) / 2 + low;	// 带符号32位整数 防止溢出翻转为负
                if (numbers[mid] == target - numbers[i]) {
                    return {i + 1, mid + 1};
                } else if (numbers[mid] > target - numbers[i]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }
        }
        return {};
    }
};
```

### [633. 平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers/)

```
class Solution {
public:
    bool judgeSquareSum(int c) {
        long a = 0,b = sqrt(c);
        while(a <= b){
            if(a*a + b*b == c){
                return true;
            }
            else if(a*a + b*b < c){
                a++;
            }
            else{
                b--;
            }
        }
        return false;
    }
};
```

### [345. 反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

```
class Solution {
public:
    string reverseVowels(string s) {
        int i=0,j=s.size()-1;   //index= length-1
        string tool="aoeiuAOEIU";
        while(i<j)
        {
            while(tool.find(s[i])==-1&&i<j) //npos = -1
                ++i;
            while(tool.find(s[j])==-1&&i<j)
                --j;
            if(i<j)
                swap(s[i++],s[j--]);
        }
        return s;
    }
};
```

### [680. 验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/)

```
class Solution {
public:
    bool validPalindrome(string s) {
        int a =0,b = s.size() - 1;
        while(a < b){
            if (s[a] == s[b]){
                a++;
                b--;
            }
            else
                return isPalindrome(s,a+1,b) || isPalindrome(s,a,b-1);
        }
        return true;
    }
    //验证是否为回文字符串
    bool isPalindrome(string s,int i,int j){
        // int i = 0, j = s.size() - 1;
        while(i < j){
            if(s[i] == s[j]){
                i++;
                j--;
            }
            else{
                return false;
            }
        }
        return true;
    }
};
```

### [88. 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int p1 = 0, p2 = 0;
        int sorted[m + n];
        int cur;
        while (p1 < m || p2 < n) {
            if (p1 == m) {
                cur = nums2[p2++];
            } else if (p2 == n) {
                cur = nums1[p1++];
            } else if (nums1[p1] < nums2[p2]) {
                cur = nums1[p1++];
            } else {
                cur = nums2[p2++];
            }
            sorted[p1 + p2 - 1] = cur;
        }
        for (int i = 0; i != m + n; ++i) {
            nums1[i] = sorted[i];
        }
    }
};
```

```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        for(int i = 0;i<n;i++,m++){
            nums1[m] =nums2[i];
        }
        sort(nums1.begin(),nums1.end());
    }
};
```

### [141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
//快慢指针 一个走两步 一个走一步
class Solution {
public:
    bool hasCycle(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return false;
        }
        ListNode* slow = head;
        ListNode* fast = head->next;
        while (slow != fast) {
            if (fast == nullptr || fast->next == nullptr) {
                return false;
            }
            slow = slow->next;
            fast = fast->next->next;
        }
        return true;
    }
};
```

### [524. 通过删除字母匹配到字典里最长单词](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/)

```
// //字典序 按英文字母顺序排序
// //长度最长 字典序最小
bool comp(string a,string b){
    if(a.size() == b.size())    {return a<b;}
    return a.size() > b.size();
}

class Solution {
public:
    bool issub(string s, string t) {
        int n = s.size(), m = t.size();
        int i = 0, j = 0;
        while (i < n && j < m) {
            if (s[i] == t[j]) {
                i++;
            }
            j++;
        }
        return i == n;
    }
    string findLongestWord(string s, vector<string>& dictionary) {
        // 更长的、字典序更小的排在前面，这样一旦找到，就是结果
        sort(dictionary.begin(), dictionary.end(),comp);
        for(string &t : dictionary) {
            if(issub(t, s)) return t;
        }
        // 如果没找到
        return "";
    }
};
```
