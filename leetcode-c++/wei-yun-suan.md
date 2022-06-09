# 位运算

按二进制位进行运算

|  &  |  按位与 |
| :-: | :--: |
|  \| |  按位或 |
|  ^  | 按位异或 |
|  \~ |  取反  |
|  << |  左移  |
|  >> |  右移  |

\_\_builtin\_popcount( ) (统计数字在二进制下“1”的个数)

[**461. 汉明距离**](https://leetcode-cn.com/problems/hamming-distance/)

```
class Solution {
public:
    int hammingDistance(int x, int y) {
        int z = x ^ y;
        int res = 0;
        while(z){
            res +=  z & 1;
            z = z >> 1; 
        }
        return res;
    }
};
//return __builtin_popcount(x^y);
```

[**136. 只出现一次的数字**](https://leetcode-cn.com/problems/single-number/)

```
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for(auto x: nums){
            res = res ^ x;
        }
        return res;
    }
};
```

#### a^0 = a (同0异1)

**a^b^a = b^a^a = b^(a^a) =b^0 = b (满足交换律结合律)**

[**268. 丢失的数字**](https://leetcode-cn.com/problems/missing-number/)

```
class Solution {
public:
    int missingNumber(vector<int>& a) {
        int res = 0;
        for(int i = 0 ;i<a.size(); i++){
            res = res^a[i]^i;
        }
        return res ^ a.size();
    }
};
```

[**260. 只出现一次的数字 III**](https://leetcode-cn.com/problems/single-number-iii/)

```
```
