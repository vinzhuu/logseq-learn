alias:: [[二叉树]]
tags:: [[Algorithm]], [[Tree]]
---

- ## 各种二叉树
	- ### 完美二叉树 (Perfect Binary Tree)
		- ![image.png](../assets/image_1722860353205_0.png){:height 279, :width 246}
	- ### 完全二叉树 (Complete Binary Tree)
		- ![image.png](../assets/image_1722860403380_0.png){:height 279, :width 246}
	- ### 完满二叉树 (Full Binary Tree)
		- ![image.png](../assets/image_1722860449646_0.png){:height 279, :width 246}
	- ### 平衡二叉树 (Balanced Binary Tree)
		- ![image.png](../assets/image_1722860839246_0.png){:height 325, :width 330}
	- ### 二叉搜索树 (Binary Search Tree, BST)
		- 对于根节点，左子树中所有节点的值 < 根节点的值 < 右子树中所有节点的值。
		  logseq.order-list-type:: number
		- 任意节点的左、右子树也是二叉搜索树，即同样满足条件 `1.` 。
		  logseq.order-list-type:: number
		- ![image.png](../assets/image_1722860997171_0.png){:height 247, :width 330}
	- ### AVL 树
		- 由 G. M. Adelson-Velsky 和 E. M. Landis 首次提出，故得此名。
		- AVL 树是一种 Balanced Binary Search Tree (平衡二叉搜索树) ，既是 Binary Search Tree, 又是 Balanced Binary Tree.
	- ### 红黑树
		- 参考: [红黑树 - 定义, 插入, 构建](https://www.bilibili.com/video/BV1Xm421x7Lg/?vd_source=f1fbb083ddef12dcff3388779faac201)
		- 红黑树的定义：
			- `左根右` : 必须是二叉搜索树
			- `根叶黑` : 根节点 和 叶子节点必须是黑色 (这里的叶子节点指的是补全的 Null 节点)
			- `不红红` : 红色节点的直接子节点不能是红色的
			- `黑路同` : 根节点到所有 Null 节点的路径上的黑色节点数相同。
		- ![image.png](../assets/image_1723105436182_0.png){:height 348, :width 523}
- ---
- ## 参考
	- [Hello 算法 - 二叉树](https://www.hello-algo.com/chapter_tree/binary_tree/)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
-