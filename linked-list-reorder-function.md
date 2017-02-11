# Linked List - Reorder Function

若給定一個單向的連結串列:

N\(1\), N\(2\), N\(3\), N\(4\), ..., N\(m-1\), N\(m\)

請實作一個演算法可以產出如下的reorder list:

N\(1\), N\(m\), N\(2\), N\(m-1\), N\(3\)...

e.g.:

Input: 1,2,3,4,5

Output: 1,5,2,4,3

**限制: 盡可能追求時間最佳化與空間最佳化**

這裡指討論最佳解, 時間複雜度為**O\(n\)**

思路:

1. 透過[龜兔賽跑演算法](https://zh.wikipedia.org/wiki/Floyd%E5%88%A4%E5%9C%88%E7%AE%97%E6%B3%95)求出中間節點, 即要對半切的那個點
2. 用剛才找到的中間點去把串列分成兩半
3. 用反序的方式重排後半段
4. 把兩半串列合起來

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/datastructures/list/LinkedList.java), 詳閱reorderList function.

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

    private LinkedNode reverseList(LinkedNode node) {
        LinkedNode previous = null;
        LinkedNode current = node;
        LinkedNode next;

        while (current != null) {
            next = current.getNext();
            current.setNext(previous);
            previous = current;
            current = next;
        }

        node = previous;
        return node;
    }

    public LinkedNode reorderList(LinkedNode node) {
        // Step1. Find the middle node bu using tortoise and hare algorithm
        LinkedNode tortoise = node;
        LinkedNode hare = tortoise.getNext();
        while (hare != null && hare.getNext() != null) {
            tortoise = tortoise.getNext();
            hare = hare.getNext().getNext();
        }

        // Step2. Split the list into two parts
        LinkedNode firstHead = node;
        LinkedNode secondHead = tortoise.getNext();
        tortoise.setNext(null);

        secondHead = reverseList(secondHead);

        node = new LinkedNode(0);

        LinkedNode current = node;
        while (firstHead != null || secondHead != null) {
            // First, add the node of first part into the list
            if (firstHead != null) {
                current.setNext(firstHead);
                current = current.getNext();
                firstHead = firstHead.getNext();
            }

            // Then, add the node of second part into the list
            if (secondHead != null) {
                current.setNext(secondHead);
                current = current.getNext();
                secondHead = secondHead.getNext();
            }
        }
        node = node.getNext();
        return node;
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

```java
@Test
    public void testReorderFunction() {
        linkedList.insertTail(1);
        linkedList.insertTail(2);
        linkedList.insertTail(3);
        linkedList.insertTail(4);
        linkedList.insertTail(5);
        linkedList.reorderList(linkedList.find(1));
        assertEquals(1, linkedList.removeHead().getId());
        assertEquals(5, linkedList.removeHead().getId());
        assertEquals(2, linkedList.removeHead().getId());
        assertEquals(4, linkedList.removeHead().getId());
        assertEquals(3, linkedList.removeHead().getId());
    }
```



