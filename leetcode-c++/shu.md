# 树

```
//Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};
```

### [104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

```
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```

### [110. 平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

```
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
    bool isBalanced(TreeNode* root) {
        if(root == nullptr) return true;
        else    return abs (maxDepth(root->left) - maxDepth(root->right)) <= 1 && isBalanced(root->left) && isBalanced(root->right);
    }
};
```

### [543. 二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

```
class Solution {
public:
    int ans = 0;
    int depth(TreeNode* root){
        if (root == NULL) return 0;
        int L = depth(root->left);
        int R = depth(root->right);
        ans = max(ans, L + R);
        return max(L, R) + 1;
    }
    int diameterOfBinaryTree(TreeNode* root) {
        depth(root);
        return ans;
    }
};
```

### [226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

```
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == nullptr) {
            return nullptr;
        }
        TreeNode* temp;
        temp = root->left ;
        root->left = root->right;
        root->right = temp;
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

### [617. 合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)

```
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if(root1 == nullptr)    return root2;
        if(root2 == nullptr)    return root1;
        root1->val = root1->val + root2->val;
        root1->left = mergeTrees(root1->left,root2->left);
        root1->right = mergeTrees(root1->right,root2->right);
        return root1;
    }
};
```

### [112. 路径总和](https://leetcode-cn.com/problems/path-sum/)

```
class Solution {
public:
    bool hasPathSum(TreeNode *root, int sum) {
        if(root == nullptr) return false;
        if(root->left == nullptr && root->right ==nullptr){
            return sum == root->val;
        }
        return hasPathSum(root->left,sum - root->val) || hasPathSum(root->right,sum - root->val);
    }
};
```

### [437. 路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)

```
```

### [572. 另一棵树的子树](https://leetcode-cn.com/problems/subtree-of-another-tree/)

```
class Solution {
public:
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(root == nullptr) return false;
        if(subRoot == nullptr ) return true;
        return isSubtree(root->left,subRoot) || isSubtree(root->right,subRoot) || issametree(root,subRoot);
    }
    bool issametree(TreeNode* root, TreeNode* root2){
        if(root == nullptr && root2 == nullptr) return true;
        if(root == nullptr || root2 == nullptr) return false;
        if(root->val != root2->val) return false;
        return(issametree(root->left,root2->left) && issametree(root->right,root2->right));
    }
};
```

### [101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

```
```

### [111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

```
```

### [404. 左叶子之和](https://leetcode-cn.com/problems/sum-of-left-leaves/)

```
```

### [687. 最长同值路径](https://leetcode-cn.com/problems/longest-univalue-path/)

```
```

### [671. 二叉树中第二小的节点](https://leetcode-cn.com/problems/second-minimum-node-in-a-binary-tree/)

```
```

### [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

```
class Solution {
public:
    void preorder(TreeNode *root, vector<int> &res) {
        if (root == nullptr)    return;
        res.push_back(root->val);
        preorder(root->left, res);
        preorder(root->right, res);
    }
    vector<int> preorderTraversal(TreeNode *root) {
        vector<int> res;
        preorder(root, res);
        return res;
    }
};
```

### [145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

```
class Solution {
public:
    void postorder(TreeNode* root, vector<int> &res){
        if(root == nullptr) return ;
        postorder(root->left,res);
        postorder(root->right,res);
        res.push_back(root->val);
    }   
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        postorder(root,res);
        return res;
    }
};
```

### [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

```
class Solution {
public:
    void inorder(TreeNode* root, vector<int> &res){
        if(root == nullptr) return ;
        inorder(root->left,res);
        res.push_back(root->val);
        inorder(root->right,res); 
    } 
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root,res);
        return res;
    }
};
```
