# 110. Balanced Binary Tree

## Problem Description

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:
> A binary tree in which the left and right subtrees of every node differ in height by no more than 1.

**Example 1:**
```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

**Example 2:**
```
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```

**Example 3:**
```
Input: root = []
Output: true
```

**Constraints:**
- The number of nodes in the tree is in the range `[0, 5000]`
- `-10^4 <= Node.val <= 10^4`

## Problem Analysis

### Key Points
- A balanced binary tree requires that for every node, the heights of its left and right subtrees differ by at most 1
- Need to check this condition for ALL nodes in the tree
- An empty tree is considered balanced
- Height of a node = max(left_height, right_height) + 1

### Approach Considerations
1. **Naive Approach**: Calculate height for each node separately - O(n²) time complexity
2. **Optimized Approach**: Calculate height and check balance in single traversal - O(n) time complexity

## Solutions

### Approach 1: Top-Down (Naive)
**Time Complexity:** O(n²)  
**Space Complexity:** O(h) where h is height of tree

### Approach 2: Bottom-Up (Optimized)
**Time Complexity:** O(n)  
**Space Complexity:** O(h) where h is height of tree

## Implementation

### C++ Solutions

```cpp
// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

// Approach 1: Top-Down (Naive) - O(n²) time
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        if (!root) return true;
        
        int leftHeight = getHeight(root->left);
        int rightHeight = getHeight(root->right);
        
        return abs(leftHeight - rightHeight) <= 1 && 
               isBalanced(root->left) && 
               isBalanced(root->right);
    }
    
private:
    int getHeight(TreeNode* node) {
        if (!node) return 0;
        return 1 + max(getHeight(node->left), getHeight(node->right));
    }
};

// Approach 2: Bottom-Up (Optimized) - O(n) time
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        return checkBalance(root) != -1;
    }
    
private:
    int checkBalance(TreeNode* node) {
        if (!node) return 0;
        
        int leftHeight = checkBalance(node->left);
        if (leftHeight == -1) return -1;  // Left subtree is unbalanced
        
        int rightHeight = checkBalance(node->right);
        if (rightHeight == -1) return -1;  // Right subtree is unbalanced
        
        // Check if current node is balanced
        if (abs(leftHeight - rightHeight) > 1) return -1;
        
        return 1 + max(leftHeight, rightHeight);
    }
};
```

## Test Cases

```cpp
#include <cassert>
#include <iostream>
using namespace std;

void test_balanced_binary_tree() {
    Solution solution;
    
    // Test Case 1: Balanced tree [3,9,20,null,null,15,7]
    TreeNode* root1 = new TreeNode(3);
    root1->left = new TreeNode(9);
    root1->right = new TreeNode(20);
    root1->right->left = new TreeNode(15);
    root1->right->right = new TreeNode(7);
    assert(solution.isBalanced(root1) == true);
    
    // Test Case 2: Unbalanced tree [1,2,2,3,3,null,null,4,4]
    TreeNode* root2 = new TreeNode(1);
    root2->left = new TreeNode(2);
    root2->right = new TreeNode(2);
    root2->left->left = new TreeNode(3);
    root2->left->right = new TreeNode(3);
    root2->left->left->left = new TreeNode(4);
    root2->left->left->right = new TreeNode(4);
    assert(solution.isBalanced(root2) == false);
    
    // Test Case 3: Empty tree
    assert(solution.isBalanced(nullptr) == true);
    
    // Test Case 4: Single node
    TreeNode* root4 = new TreeNode(1);
    assert(solution.isBalanced(root4) == true);
    
    // Test Case 5: Left skewed tree [1,2,null,3,null,4]
    TreeNode* root5 = new TreeNode(1);
    root5->left = new TreeNode(2);
    root5->left->left = new TreeNode(3);
    root5->left->left->left = new TreeNode(4);
    assert(solution.isBalanced(root5) == false);
    
    cout << "All test cases passed!" << endl;
}

int main() {
    test_balanced_binary_tree();
    return 0;
}
```

## Related Problems

- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

## Tags
- Binary Tree
- Tree Traversal
- Depth-First Search (DFS)
- Recursion
- Tree Height/Depth

## Difficulty
Easy

## Notes
- Remember to handle edge cases (empty tree, single node)
- Consider both time and space complexity optimizations
- The bottom-up approach is more efficient as it avoids redundant height calculations

---

## TODO
- [ ] Add complete solution implementations
- [ ] Add detailed explanation of algorithms
- [ ] Add complexity analysis for each approach
- [ ] Add visual diagrams
- [ ] Add more test cases
- [ ] Add iterative solutions
- [ ] Add variations
