# Ordered Linked List\(有序連結串列\)

就是list中的資料是排好順序的喇

效能: 插入和刪除都要O\(n\)的時間複雜度

以下是比較粗糙的實作\(升冪排列\), 只使用有單向連結串列, 所以省略了從尾部新增節點的操作

```java
package idv.carl.datastructures.list;

/**
 * @author Carl Lu
 */
public class OrderedLinkedList {
    private LinkedNode head;
    private int size = 0;

    public void insertHead(int id) {
        LinkedNode newNode = new LinkedNode(id);

        // Need to find the correct location for insert operation
        LinkedNode previous = null;
        LinkedNode current = head;

        // Order the list ascending by id
        while (current != null && id > current.getId()) {
            previous = current;
            current = current.getNext();
        }

        if (previous == null) {
            head = newNode;
        } else {
            previous.setNext(newNode);
        }

        newNode.setNext(current);
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

使用有序連結串列

