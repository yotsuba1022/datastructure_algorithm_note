# Linked List\(連結串列\)

Linked List也是一種特殊的線性表, 其由一系列的節點組成, 節點的順序是通過節點元素中的指標連接次序來確定的. Linked List中的節點包含兩個部分, 一個是其自身需存放的資料, 另一個是指向下一個節點的參照\(reference\).

Linked List v.s. Arry

1. 都可作為資料的儲存結構
2. Array: 固定長度, 依序存放
3. Linked List: 無容量限制, 非連續和非順序的儲存結構
4. 從效率上來說, linked list基本上是優於array的
5. 基本上, 只要是能用array的地方, 都可以用linked list來代替array. Linked list的缺點是引入了複雜度.

Linked List的基本操作

1. 向list中插入資料
2. 從list中移除資料
3. 查看list中所有的資料
4. 查詢指定的節點
5. 刪除指定的節點

Linked List的效能

1. 在表頭插入和刪除非常快, 基本就是修改一下參照值, 時間大約為常量, 即O\(1\).
2. 若為查詢/刪除特定節點, 大約需要O\(n\)次比較, 跟陣列差不多, 但仍然比陣列快, 因為它不需要移動或複製資料.

```java
package idv.carl.datastructures.list;

/**
 * @author Carl Lu
 */
public class LinkedList {

    private LinkedNode head;
    private int size = 0;

    public void insertHead(int id) {
        LinkedNode newNode = new LinkedNode(id);
        newNode.setNext(head);
        head = newNode;
        size++;
    }

    public void insertTail(int id) {
        LinkedNode newNode = new LinkedNode(id);

        if (head == null) {
            head = newNode;
            size++;
            return;
        }

        LinkedNode tail = head;

        while (tail.getNext() != null) {
            tail = tail.getNext();
        }
        tail.setNext(newNode);
        size++;
    }

    public LinkedNode removeHead() {
        if (size == 0) {
            return null;
        }

        LinkedNode tmp = head;
        head = head.getNext();
        size--;
        return tmp;
    }

    public LinkedNode find(int id) {
        LinkedNode node = head;
        while (node.getId() != id) {
            if (node.getNext() == null) {
                return null;
            } else {
                node = node.getNext();
            }
        }
        return node;
    }

    public LinkedNode remove(int id) {
        if (size == 0) {
            return null;
        }

        LinkedNode deleted = head;
        LinkedNode previous = head;

        // To search the deleted node and it's previous node
        while (deleted.getId() != id) {
            if (deleted.getNext() == null) {
                return null;
            } else {
                previous = deleted;
                deleted = deleted.getNext();
            }
        }

        // Reset the relationship of nodes
        if (deleted.equals(head)) {
            head = head.getNext();
        } else {
            previous.setNext(deleted.getNext());
        }

        size--;
        return deleted;
    }

    public void displayList() {
        LinkedNode tmp = head;
        while (tmp != null) {
            System.out.println(tmp.toString());
            tmp = tmp.getNext();
        }
    }

    public int getSize() {
        return size;
    }
}

```



