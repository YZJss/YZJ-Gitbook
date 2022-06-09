# 动态规划

```python
# 初始化 base case
dp[0][0][...] = base case
for 状态1 in 状态1的所有取值：
    for 状态2 in 状态2的所有取值：
        for ...
            dp[状态1][状态2][...] = 求最值(选择1，选择2...)
```

### [509. 斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)

```
class Solution {
public:
    int fib(int n) {
        if(n == 0)  return 0;
        if(n == 1)  return 1;
        vector<int> dp(n+1);
        dp[0] = 0;
        dp[1] = 1;
        for(int i = 2;i<n+1;i++){
            dp[i] = dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
};
```

```
class Solution {
public:
    int fib(int n) {
        int ans = 0;
        if(n == 0)  return 0;
        if(n == 1)  return 1;
        int p = 0;
        int q = 1;
        for(int i = 2;i<n+1;i++){
            ans = p + q;
            p = q;
            q = ans;
        }
        return ans;
    }
};
```

### [322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/)

```
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1,amount + 1);
        dp[0] = 0;
        for(int i = 1;i <= amount;i++){
            for(auto &x : coins){
                if(i - x >= 0){
                    dp[i] = min(dp[i],dp[i-x] + 1);
                }
            }
        }
        return dp[amount] == amount + 1 ? -1 : dp[amount];
    }
};
```

### [300. 最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

```
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> dp(nums.size() +1,1);
        for(int i = 0;i < nums.size() ;i++){
            for(int j = 0; j < i;j++){
                if(nums[j] < nums[i]){
                    dp[i] = max(dp[i],dp[j] + 1);
                }
            }
        }
        return *max_element(dp.begin(),dp.end());
    }
};
```

### [72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)

```
int tmin(int a,int b,int c){
    return min(a,min(b,c));
}

class Solution {
public:
    int minDistance(string word1, string word2) {
        int a = word1.size();
        int b = word2.size();
        vector<vector<int>> dp(a + 1,vector<int>(b + 1));
        for(int i = 0;i<= a;i++){
            dp[i][0] = i;
        }
        for(int i = 0;i<= b;i++){
            dp[0][i] = i;
        }
        for(int i = 1;i <=a;i++){
            for(int j = 1;j <=b;j++){
                if(word1[i-1] == word2[j-1])
                    dp[i][j] = dp[i-1][j-1];
                else
                    dp[i][j] = tmin(dp[i-1][j-1],dp[i-1][j],dp[i][j-1])+1;
            }
        }
        return dp[a][b];
    }
};
```

### [53. 最大子数组和](https://leetcode-cn.com/problems/maximum-subarray/)

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp(nums.size());
        dp[0] = nums[0];
        for(int i = 1; i< nums.size();i++)
            dp[i] = max(dp[i-1]+nums[i],nums[i]);
        return *max_element(dp.begin(),dp.end());
    }
};
```

### [1143. 最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)

一个字符串的 **子序列** 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。

```
class Solution {
public:
    int longestCommonSubsequence(string t1, string t2) {
        int a= t1.size();
        int b = t2.size();
        vector<vector<int>> dp(a+1,vector<int>(b+1,0));
        for(int i = 1;i<=a;i++){
            for(int j = 1; j<=b;j++){
                if(t1[i-1] == t2[j-1])
                    dp[i][j] = dp[i-1][j-1]+1;
                else
                    dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
            }
        }
        return dp[a][b];
    }
};
```

#### 0-1 背包

可装载重量为 `W` ， `N` 个物品的背包。其中第 `i` 个物品的重量为 `wt[i]`，价值为 `val[i]`，现在让你用这个背包装物品，最多能装的价值是多少？

```
int knapsack(int w, int n, vector<int> wt, vector<int> val){
    vector<vector<int> > dp(n+1,vector<int>(w+1,0));
    for(int i = 1;i<=n;i++){
        for(int j = 1;j<=w;j++){
            if(j - wt[i-1] < 0){
                dp[i][j] = dp[i-1][j];
            }
            else{
                dp[i][j] = max(dp[i-1][j-wt[i-1]] + val[i-1],dp[i-1][j]);
            }
        }
    }
    return dp[n][w];
}

int main() {
    int n = 3,w = 4;
    vector<int> wt = {2,1,3};
    vector<int> val = {4,2,3};
    int ans = knapsack(w,n,wt,val);
    cout << ans << endl;
    return 0;
}
```

### [416. 分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

```
//转换为背包问题 先求sum 		背包容量 sum/2 恰好装满sum/2 size个物品
//dp[i][j]	前i件物品 刚好装满j
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(),nums.end(),0);
        if(sum % 2 != 0)    return false;
        int size = nums.size();
        sum = sum / 2;
        vector<vector<int>> dp(size + 1,vector<int>(sum + 1));
        for (int i = 0; i <= size; i++) {
            dp[i][0] = true;
        }
        for (int i = 1; i <= size; i++) {
            for (int j = 1; j <= sum; j++) {
                if (j - nums[i - 1] < 0) {
                    dp[i][j] = dp[i - 1][j];
                } 
                else{
                    dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
                }
            }
        }
        return dp[size][sum];
    }
};
```

### [518. 零钱兑换 II](https://leetcode.cn/problems/coin-change-2/)

### [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)

```
class Solution {
public:
    int minPathSum(vector<vector<int>>& a) {
        int m = a.size();
        int n = a[0].size();
        vector<vector<int>> dp(m,vector<int>(n));
        dp[0][0] = a[0][0];
        for(int i= 1;i<m;i++){
            dp[i][0] = dp[i-1][0] + a[i][0];
        }
        for(int i= 1;i<n;i++){
            dp[0][i] = dp[0][i-1] + a[0][i];
        }
        for(int i = 1; i<m;i++){
            for(int j = 1; j<n;j++){
                dp[i][j] = min(dp[i-1][j]+a[i][j],dp[i][j-1]+a[i][j]);
            }
        }
        return dp[m-1][n-1];
    }
};
```

### [10. 正则表达式匹配](https://leetcode.cn/problems/regular-expression-matching/)

`'.'` 匹配任意单个字符

`'*'` 匹配零个或多个前面的那一个元素

```
```

### [312. 戳气球](https://leetcode.cn/problems/burst-balloons/)

```
```

[**70. 爬楼梯**](https://leetcode-cn.com/problems/climbing-stairs/)

```
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp(n+1);
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```
