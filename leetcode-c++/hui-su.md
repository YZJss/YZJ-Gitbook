# 回溯

```python
result = []
def backtrack(路径, 选择列表):
	if 满足结束条件:
    result.add(路径)
    return
 	for 选择 in 选择列表:
    # 做选择
    将该选择从选择列表移除 used[]
    路径.add(选择)
    backtrack(路径, 选择列表)
    #撤销选择
    路径.remove(选择)
    将该选择再加入选择列表	used[]
```

[**46. 全排列**](https://leetcode-cn.com/problems/permutations/)

```
class Solution {
public:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking (vector<int>& nums, vector<bool>& used) {
        // 此时说明找到了一组
        if (path.size() == nums.size()) {
            result.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            if (used[i] == true) continue; // path里已经收录的元素，直接跳过
            path.push_back(nums[i]);
            used[i] = true;
            backtracking(nums, used);
            path.pop_back();
            used[i] = false;
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<bool> used(nums.size(), false);
        backtracking(nums, used);
        return result;
    }
};
```
