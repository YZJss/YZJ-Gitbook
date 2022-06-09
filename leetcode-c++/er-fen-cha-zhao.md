# 二分查找

### [69. x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

```
class Solution {
public:
    int mySqrt(int x) {
        int l = 0, r = x, ans = -1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if ((long long)mid * mid <= x) {
                ans = mid;
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return ans;
    }
};
```

### [744. 寻找比目标字母大的最小字母](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/)

```
class Solution {
public:
    char nextGreatestLetter(vector<char>& l, char t) {
        int left = 0,right = l.size() - 1;
        while(left <= right){
            int mid = left+(right-left)/2;
            if(l[mid] <= t){
                left = mid + 1;
            }
            else{
                right = mid - 1;
            }
        }
        if(left < l.size()){
            return l[left];
        }else{
            return l[0];
        }
    }
};
```

### [540. 有序数组中的单一元素](https://leetcode-cn.com/problems/single-element-in-a-sorted-array/)

```
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        while (left < right){
            int mid = left + (right-left)/2;
            if(mid % 2 == 0){
                if(nums[mid] == nums[mid+1]){
                    left = mid + 1;
                }
                else{
                    if (mid == 0 || nums[mid-1] != nums[mid]) return nums[mid];
                    right = mid - 1;
                }
            }
            else{
                if (nums[mid] == nums[mid-1]) {
                    left = mid + 1;
                } else {
                    if (nums[mid] != nums[mid+1]) return nums[mid];
                    right = mid - 1;
                }
            }
        }
        return nums[left];
    }
};
```

### [278. 第一个错误的版本](https://leetcode-cn.com/problems/first-bad-version/)

```
class Solution {
public:
    int firstBadVersion(int n) {
        int left = 1,right = n;
        while(left < right){
            int mid = left + (right-left)/2;
            if(isBadVersion(mid)){
                right = mid; 
            }
            else{
                left = mid + 1;
            }
        }
        return left;
    }
};
```

### [153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

```
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        while(left < right){
            int mid = left + (right - left) / 2;
            if(nums[mid] > nums[right]){
                left = mid + 1;
            }
            else{
                right = mid;
            }
        }
        return nums[left];
    }
};
```

[题解](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/solution/er-fen-cha-zhao-wei-shi-yao-zuo-you-bu-dui-cheng-z/)

### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        if(nums.empty()) return {-1,-1};
        int l = 0, r = nums.size() - 1; //二分范围
        while( l < r)			        //查找元素的开始位置
        {
            int mid = (l + r )/2;
            if(nums[mid] >= target) r = mid;
            else l = mid + 1;
        }
        if( nums[r] != target) return {-1,-1};  //查找失败
        int L = r;
        l = 0, r = nums.size() - 1;     //二分范围
        while( l < r)                   //查找元素的结束位置
        {
            int mid = (l + r + 1)/2;
            if(nums[mid] <= target ) l = mid;
            else r = mid - 1;
        }
        return {L,r};
    }
};
```
