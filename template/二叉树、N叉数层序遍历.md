#### [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

难度中等1114收藏分享切换为英文接收动态反馈

给你一个二叉树，请你返回其按 **层序遍历** 得到的节点值。 （即逐层地，从左到右访问所有节点）。

 

**示例：**
二叉树：`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层序遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```



### Solution

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        
        if(root == null) {
            return Collections.emptyList();
        }

        List<List<Integer>> ans = new ArrayList<>();

        // 层序遍历使用队列辅助
        Queue<Pair> queue = new LinkedList<>();
        queue.add(new Pair(root, 0));

        while(!queue.isEmpty()) {
            Pair pair = queue.poll();
            Integer depth = pair.depth;
            TreeNode node = pair.node;

            if (depth >= ans.size()) {
                ans.add(new ArrayList<>());
            }

            ans.get(depth).add(node.val);

            if (node.left != null) {
                queue.add(new Pair(node.left, depth + 1));
            }
            if (node.right != null) {
                queue.add(new Pair(node.right, depth + 1));
            }
        }

        return ans;
    }

    public static class Pair {

        public TreeNode node;
        public Integer depth;
        
        public Pair(TreeNode node, Integer depth) {
            this.node = node;
            this.depth = depth;
        }
    }
}
```





<hr/>



#### [429. N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

难度中等186收藏分享切换为英文接收动态反馈

给定一个 N 叉树，返回其节点值的*层序遍历*。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[[1],[3,2,4],[5,6]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

 

**提示：**

- 树的高度不会超过 `1000`
- 树的节点总数在 `[0, 10^4]` 之间



### Solution

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        
        if (root == null) {
            return Collections.emptyList();
        }

        List<List<Integer>> ans = new ArrayList<>();
        Queue<Pair> queue = new LinkedList<>();

        queue.add(new Pair(root, 0));

        while(!queue.isEmpty()) {

            Pair pair = queue.poll();
            Node node = pair.node;
            int depth = pair.depth;

            if(depth >= ans.size()) {
                ans.add(new ArrayList<>());
            }
            ans.get(depth).add(node.val);

            for (Node child : node.children) {
                queue.add(new Pair(child, depth + 1));
            }
        }

        return ans;

    }

    public static class Pair{
        Node node;

        int depth;

        public Pair(Node node, int depth) {
            this.node = node;
            this.depth = depth;
        }
    }
}
```

