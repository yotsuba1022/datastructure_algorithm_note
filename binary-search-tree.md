### 二元搜尋樹\(Binary Search Tree, BST\)

#### 定義: 若一顆二元樹滿足以下兩點:

a. 左子節點的值小於節點的值

b. 右子節點的值大於節點的值

即可稱為二元搜尋樹

```
     2            6
    / \          / \
   1   3        5   8     <-----像這樣, 這兩棵都是BST
               /   / \
              3   7   9
```

二元搜尋樹的查詢, 插入, 走訪, 查詢最大最小值和刪除操作

提示: 刪除節點有兩個子節點的時候, 要用它的中序後繼來代替該節點,

**演算法為: 找到被刪除節點的右子節點, 然後查詢此右子節點下的最後一個左子節點, 即此顆子樹的最小值節點, 這就是被刪除節點的中序後繼節點.   **

何謂前序, 中序, 後序?

以上圖右邊的三層樹為例, 看1~2層的子樹:

前序: 6 -&gt; 5 -&gt; 8

中序: 5 -&gt; 6 -&gt; 8

後序: 5 -&gt; 8 -&gt; 6

若看整顆:

中序: 3 -&gt; 5 -&gt; 6 -&gt; 7 -&gt; 8 -&gt; 9

所以若要刪除8, 要找它的“中序後繼節點\(in-order successor\)”的話, 就是9了

### 二元搜尋樹操作的效率

#### 常見的時間複雜度為: O\(logN\), 是以2為底的

### 用陣列來表示樹

把樹的節點打上編號, 按順序放到陣列中. 如此一來, 查找節點就變成了查找相應的索引了. 這種方法不常用, 了解即可.

此種方式效率不高, 因為不滿的節點還有刪除的節點, 在陣列中留下了多餘的空間, 這是一種記憶體上的浪費, 更糟糕的是要刪除節點時, 若要移動子樹的話, 就更浪費時間了.

關於BST的實作, 可以看這裡\([點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/datastructures/binarytree/BinaryTree.java)\)

以下是針對實作中的getSuccessor\(\)的部分做圖示說明

初始化:

```
             6

            / \

           5   8 deletedNode = successor = successorParent

          /   / \

         3   7   10 current = deletedNode.getRight\(\)

                / \

               9   11
```

```
// Find the node

             6

            / \

           5   8 successorParent = successor

          /   / \

         3   7   10 successor = current

                / \

               9   11

               ^---------- current = current.getLeft\(\)





             6

            / \

           5   8 deletedNode

          /   / \

         3   7   10 successorParent = successor

                / \

               9   11

               ^------- successor = current

                        current = current.getLeft\(\) = null



// Set related value

             6

            / \

           5   9 successor.setRight(deletedNode.getRight())

          /   / \

         3   7   10 successorParent.setLeft(successor.getRight())

                / \

              null 11                                          
```

### 



