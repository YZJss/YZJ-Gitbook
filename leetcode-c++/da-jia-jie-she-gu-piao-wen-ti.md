# 打家劫舍 股票问题

### [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)

```
//前i间房最大金额 抢、不抢
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size() == 1){
            return nums[0];
        }
        vector<int> dp(nums.size());
        int res = 0;
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for(int i = 2;i < nums.size();i++){
            dp[i] = max(dp[i - 2] + nums[i], dp[i - 1]);
        }
        return dp[nums.size() - 1];
    }
};
```

### [213. 打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

```
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size() == 1)    return nums[0];
        if(nums.size() == 2)    return max(nums[0],nums[1]);
        return max(robrange(nums,0,nums.size() - 2),robrange(nums,1,nums.size() - 1));
    }
    int robrange(vector<int> &nums , int s , int e){
        int f = nums[s], res = max(nums[s],nums[s + 1]);
        for(int i = s + 2; i < e + 1;i++){
            int temp = res;
            res = max(f + nums[i],res);
            f = temp;
        }
        return res;
    }
};
```

### [337. 打家劫舍 III](https://leetcode.cn/problems/house-robber-iii/)

```



```

### [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

```
class Solution {
public:
    int maxProfit(vector<int>& p) {
        int minprice = 1e9;
        int maxprofit = 0;
        for(int i = 0;i<p.size();i++){
            maxprofit = max(maxprofit,p[i] - minprice);
            minprice = min(minprice,p[i]);
        }
        return maxprofit;
    }
};
```

```
// 第一位 i天数 第二位 k至今最多交易数 第三位 0未持有 1持有
// dp[i][k][0] = max(dp[i-1][k][0],dp[i-1][k-1][1] + p[i])
// dp[i][k][1] = max(dp[i-1][k][1],dp[i-1[k-1][0] - p[i])

// dp[0][0][0] = 0
// dp[i][0][1] = -inf

// k 都是 1 无影响
class Solution {
public:
    int maxProfit(vector<int>& p) {
        int n = p.size();
        vector<vector<int>> dp(n,vector<int>(2));
        dp[0][0] = 0;
        dp[0][1] = -p[0];
        for(int i = 1;i < n;i++){
            dp[i][0] = max(dp[i-1][0],dp[i-1][1] + p[i]);
            dp[i][1] = max(dp[i-1][1], - p[i]);
        }
        return dp[n-1][0];
    }
};
```

### [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

```
// k = +inf 无影响
class Solution {
public:
    int maxProfit(vector<int>& p) {
        int n = p.size();
        vector<vector<int>> dp(n,vector<int>(2));
        dp[0][0] = 0;
        dp[0][1] = -p[0];
        for(int i = 1;i < n;i++){
            dp[i][0] = max(dp[i-1][0],dp[i-1][1] + p[i]);
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] - p[i]);
        }
        return dp[n-1][0];
    }
};
```

### [123. 买卖股票的最佳时机 III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)

```
```

### [188. 买卖股票的最佳时机 IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)

```
```

### [309. 最佳买卖股票时机含冷冻期](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

```
```
