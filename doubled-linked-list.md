# Double Linked List\(雙向連結串列\)

Double Linked List: 即list中的各個節點都同時紀錄著其前面與後面的節點, 這樣既能向前迭代資料, 同時也能向後迭代資料.

注意各個方法裡面如何處理節點之間的關係, 像remove by id就要考慮許多edge case不然unit test不會過.

```java
package idv.carl.datastructures.list;

/**
 * @author Carl Lu
 */
public class DoubleLinkedList {

    private DoubleLinkedNode head;
    private DoubleLinkedNode tail;
    private int size = 0;

    public void insertHead(int id) {
        DoubleLinkedNode newNode = new DoubleLinkedNode(id);
        if (isEmpty()) {
            tail = newNode;
        } else {
            head.setPrevious(newNode);
            newNode.setNext(head);
        }
        head = newNode;
        size++;
    }

    public void insertTail(int id) {
        DoubleLinkedNode newNode = new DoubleLinkedNode(id);
        if (isEmpty()) {
            head = newNode;
        } else {
            tail.setNext(newNode);
            newNode.setPrevious(tail);
        }
        tail = newNode;
        size++;
    }

    public DoubleLinkedNode removeHead() {
        if (isEmpty()) {
            return null;
        }
        DoubleLinkedNode removed = head;
        if (head.getNext() == null) {
            tail = null;
        } else {
            head.getNext().setPrevious(null);
            head = head.getNext();
        }
        size--;
        return removed;
    }

    public DoubleLinkedNode find(int id) {
        DoubleLinkedNode node = head;
        while (node != null && node.getId() != id) {
            if (node.getNext() == null) {
                return null;
            } else {
                node = node.getNext();
            }
        }
        return node;
    }

    public DoubleLinkedNode removeTail() {
        if (isEmpty()) {
            return null;
        }
        DoubleLinkedNode removed = tail;
        if (removed.getPrevious() == null) {
            head = null;
            tail = null;
        } else {
            removed.getPrevious().setNext(null);
            tail = removed.getPrevious();
        }
        size--;
        return removed;
    }

    public DoubleLinkedNode remove(int id) {
        if (isEmpty()) {
            return null;
        }
        DoubleLinkedNode removed = find(id);
        if (removed == null) {
            return removed;
        } else if (size == 1) {
            head = null;
            tail = null;
        } else if (removed == head) {
            head = head.getNext();
            head.setPrevious(null);
        } else if (removed == tail) {
            tail = removed.getPrevious();
            tail.setNext(null);
        } else {
            removed.getPrevious().setNext(removed.getNext());
            removed.getNext().setPrevious(removed.getPrevious());
        }
        size--;
        return removed;
    }

    public boolean insertAfter(int targetId, int id) {
        if (isEmpty()) {
            return false;
        }
        DoubleLinkedNode target = find(targetId);
        DoubleLinkedNode newNode = new DoubleLinkedNode(id);
        if (target == null) {
            return false;
        } else if (target == tail) {
            newNode.setPrevious(tail);
            tail.setNext(newNode);
            tail = newNode;
        } else {
            newNode.setNext(target.getNext());
            target.getNext().setPrevious(newNode);
            newNode.setPrevious(target);
            target.setNext(newNode);
        }
        size++;
        return true;
    }

    public DoubleLinkedNode peekHead() {
        return head;
    }

    public int getSize() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void displayForward() {
        DoubleLinkedNode tmp = head;
        while (tmp != null) {
            System.out.println(tmp.toString());
            tmp = tmp.getNext();
        }
    }

    public void displayBackward() {
        DoubleLinkedNode tmp = tail;
        while (tmp != null) {
            System.out.println(tmp.toString());
            tmp = tmp.getPrevious();
        }
    }

}
```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/datastructures/list/DoubleLinkedList.java)  


單元測試組合

```java
package idv.carl.datastructure.list;

import static org.junit.Assert.*;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import idv.carl.datastructures.list.DoubleLinkedList;

/**
 * @author Carl Lu
 */
public class DoubleLinkedListTest {

    private DoubleLinkedList doubleLinkedList;

    @Before
    public void init() {
        doubleLinkedList = new DoubleLinkedList();
    }

    @After
    public void destroy() {
        doubleLinkedList = null;
    }

    @Test
    public void testInsertHead() {
        doubleLinkedList.insertHead(1);
        doubleLinkedList.insertHead(5);
        doubleLinkedList.insertHead(2);
        assertEquals(3, doubleLinkedList.getSize());
        assertEquals(2, doubleLinkedList.removeHead().getId());
        assertEquals(5, doubleLinkedList.removeHead().getId());
        assertEquals(1, doubleLinkedList.removeHead().getId());
        assertEquals(0, doubleLinkedList.getSize());
    }

    @Test
    public void testInsertTail() {
        doubleLinkedList.insertTail(1);
        doubleLinkedList.insertTail(7);
        doubleLinkedList.insertTail(5);
        doubleLinkedList.displayForward();
        doubleLinkedList.displayBackward();
        assertEquals(3, doubleLinkedList.getSize());
        assertEquals(1, doubleLinkedList.removeHead().getId());
        assertEquals(7, doubleLinkedList.removeHead().getId());
        assertEquals(5, doubleLinkedList.removeHead().getId());
        assertEquals(0, doubleLinkedList.getSize());
    }

    @Test
    public void testFind() {
        assertEquals(null, doubleLinkedList.find(1));
        doubleLinkedList.insertHead(1);
        doubleLinkedList.insertTail(3);
        doubleLinkedList.insertHead(2);
        assertEquals(3, doubleLinkedList.getSize());
        assertEquals(1, doubleLinkedList.find(1).getId());
    }

    @Test
    public void testRemoveTail() {
        doubleLinkedList.insertHead(1);
        doubleLinkedList.insertHead(2);
        doubleLinkedList.insertHead(8);
        assertEquals(3, doubleLinkedList.getSize());
        assertEquals(1, doubleLinkedList.removeTail().getId());
        assertEquals(2, doubleLinkedList.getSize());
        doubleLinkedList.removeTail();
        doubleLinkedList.removeTail();
        assertNull(doubleLinkedList.peekHead());
        assertTrue(doubleLinkedList.isEmpty());
    }

    @Test
    public void testRemoveById() {
        doubleLinkedList.insertHead(10);
        doubleLinkedList.insertHead(3);
        doubleLinkedList.insertHead(99);
        doubleLinkedList.insertHead(5);
        assertEquals(4, doubleLinkedList.getSize());
        assertEquals(5, doubleLinkedList.remove(5).getId());
        assertEquals(3, doubleLinkedList.getSize());
        assertEquals(99, doubleLinkedList.peekHead().getId());
        assertEquals(10, doubleLinkedList.remove(10).getId());
        assertEquals(2, doubleLinkedList.getSize());
        assertEquals(99, doubleLinkedList.removeHead().getId());
        assertEquals(1, doubleLinkedList.getSize());
        assertEquals(null, doubleLinkedList.remove(87));
        assertEquals(1, doubleLinkedList.getSize());
        assertEquals(3, doubleLinkedList.remove(3).getId());
        assertEquals(0, doubleLinkedList.getSize());
        assertNull(doubleLinkedList.peekHead());
    }

    @Test
    public void testInsertAfter() {
        assertFalse(doubleLinkedList.insertAfter(1, 2));
        doubleLinkedList.insertHead(1);
        doubleLinkedList.insertAfter(1, 2);
        assertEquals(2, doubleLinkedList.removeTail().getId());
        doubleLinkedList.insertTail(3);
        doubleLinkedList.insertAfter(3, 5);
        assertEquals(5, doubleLinkedList.removeTail().getId());
        doubleLinkedList.insertAfter(1, 7);
        assertEquals(1, doubleLinkedList.removeHead().getId());
        assertEquals(7, doubleLinkedList.removeHead().getId());
        assertEquals(3, doubleLinkedList.peekHead().getId());
    }

}

```



