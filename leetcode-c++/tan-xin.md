# 贪心

### [455. 分发饼干](https://leetcode-cn.com/problems/assign-cookies/)

```
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(),g.end());
        sort(s.begin(),s.end());
        int i = 0,j = 0;
        while(i<g.size() && j<s.size()){
            if(s[j] >= g[i])
                i++;
            j++;
        }
        return i;

    }
};
```

### [435. 无重叠区间](https://leetcode-cn.com/problems/non-overlapping-intervals/)

```
bool comp(vector<int> &a,vector<int> &b){
    return a[1] < b[1];
}
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& a) {
        if(a.size() == 0) return 0;
        sort(a.begin(),a.end(),comp);
        int count = 1;
        int end = a[0][1];
        for(int i = 1;i<a.size();i++){
            if(end <= a[i][0]){
                end = a[i][1];
                count++;
            }
        }
        return a.size() - count;
    }
};
```

![435.无重叠区间](https://cdn.jsdelivr.net/gh/YZJss/tuchuang@main/1631930017-fYYUAr-file\_1631930017753-20220301110424392.png)

### [452. 用最少数量的箭引爆气球](https://leetcode-cn.com/problems/minimum-number-of-arrows-to-burst-balloons/)

```
bool comp(vector<int> &a,vector<int> &b){
    return a[1] < b[1];
}
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& a) {
    if(a.size() == 0) return 0;
        sort(a.begin(),a.end(),comp);
        int count = 1;
        int end = a[0][1];
        for(int i = 1;i<a.size();i++){
            if(end < a[i][0]){
                end = a[i][1];
                count++;
            }
        }
        return count;
    }
};
```

### [406. 根据身高重建队列](https://leetcode-cn.com/problems/queue-reconstruction-by-height/)

```
bool comp(vector<int> &a,vector<int> &b){
    if(a[0] != b[0]) return a[0] > b[0];
    return a[1] < b[1];
}
class Solution {
public:
    vector<vector<int>> reconstructQueue(vector<vector<int>>& p) {
        sort(p.begin(),p.end(),comp);
        vector<vector<int> > ans;
        for(int i = 0;i<p.size();i++){
            int pos = p[i][1];
            ans.insert(ans.begin()+pos,p[i]);
        }
        return ans;
    }
};
```

### [605. 种花问题](https://leetcode-cn.com/problems/can-place-flowers/)

```
class Solution {
public:
    bool canPlaceFlowers(vector<int>& f, int n) {
        int cnt = 0;
        for(int i = 0; cnt < n && i < f.size(); i++){
            if(f[i] == 1){
                continue;
            }
            int pre = i == 0 ? 0 : f[i-1];
            int next = i == f.size() - 1 ? 0 : f[i+1];
            if(pre == 0 && next == 0){
                cnt++;
                f[i] = 1;
            }
        }
        return cnt >= n;
    }
};
```

### [392. 判断子序列](https://leetcode-cn.com/problems/is-subsequence/)

```
class Solution {
public:
    bool isSubsequence(string s, string t) {
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
};
```

### [665. 非递减数列](https://leetcode-cn.com/problems/non-decreasing-array/)

```
class Solution {
public:
    bool checkPossibility(vector<int>& nums) {
        int n = nums.size(),cnt = 0;
        for(int i = 1 ;i < n ; i++){
            if(nums[i-1] <= nums[i]){
                continue;
            }
            cnt++;
            if (i-2>=0 && nums[i-2] > nums[i]){
			    nums[i] = nums[i-1];
		    }
            else{
			    nums[i-1] = nums[i];
		    }
        }
    return cnt < 2;
    }
};
```

### [53. 最大子数组和](https://leetcode-cn.com/problems/maximum-subarray/)

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int pre = 0, maxans = INT_MIN;
        for(int i = 0; i< nums.size(); i++){
            pre = max(pre + nums[i],nums[i]);
            maxans = max(maxans,pre);
        }
        return maxans;
    }
};
```

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp (nums.size());
        int res = INT_MIN;
        dp[0] = nums[0];
        for(int i = 1; i< nums.size();i++){
            if(dp[i - 1] > 0){
                dp[i] = dp[i - 1]+ nums[i];
            }
            else{
                dp[i] = nums[i];
            }
        }
        for(int i = 0; i< dp.size();i++){
            res = max(res,dp[i]);
        }
        return res;
    }
};
```

### [763. 划分字母区间](https://leetcode-cn.com/problems/partition-labels/)

```
class Solution {
public:
    vector<int> partitionLabels(string S) {
        int hash[27] = {0};
        for (int i = 0; i < S.size(); i++) {
            hash[S[i] - 'a'] = i;
        }
        vector<int> result;
        int left = 0;
        int right = 0;
        for (int i = 0; i < S.size(); i++) {
            right = max(right, hash[S[i] - 'a']); 
            if (i == right) {
                result.push_back(right - left + 1);
                left = i + 1;
            }
        }
        return result;
    }
};
```

![763.划分字母区间](https://cdn.jsdelivr.net/gh/YZJss/tuchuang@main/1631930197-jioLfX-file\_1631930197652.png)

### [56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/)

```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& in) {
        sort(in.begin(),in.end());
        vector<vector<int> > res;
        for(int i = 0;i<in.size();){
            int t = in[i][1];
            int j = i+1;
            while(j<in.size() && t >= in[j][0]){
                t = max(t,in[j][1]);
                j++;
            }
            res.push_back({in[i][0],t});
            i = j;
        }
        return res;
    }
};
```

### [57. 插入区间](https://leetcode-cn.com/problems/insert-interval/)

```
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& in, vector<int>& ne) {
        vector<vector<int> > res;
        if(in.size() == 0)  return {ne};
        int i = 0;
        while(i < in.size() && in[i][1] < ne[0]){
            res.push_back(in[i++]);
        }
        while(i < in.size() && in[i][0] <= ne[1]){
            ne[0] = min(in[i][0],ne[0]);
            ne[1] = max(in[i][1],ne[1]);
            i++;
        }
        res.push_back(ne);
        while(i < in.size()){
            res.push_back(in[i++]);
        }
        return res;
    }
};
```
