# Queue\(佇列\)

什麼是Queue: Queue是一種特殊的線性表, 限定只能在表的一端進行插入\(隊尾\), 而在另一端進行刪除操作\(隊頭\), 特點是"先進先出"\(FIFO\).

Queue的基本操作:

1. insert:在隊尾插入資料
2. remove: 從隊頭移走資料
3. peek: 查看隊頭的資料

Circular Queue: 為了避免queue未滿, 卻不能插入新資料項的問題, 可以讓隊頭隊尾的指標繞回陣列開始的位置, 這就是circular queue, 又稱作ring buffer.

Queue的效能: insert和remove的時間複雜度均為O\(1\)

一個簡單的circular queue的實作\(原始碼點我\):

```java
package idv.carl.datastructures.queue;

/**
 * @author Carl Lu
 */
public class CircularQueue {
    private int[] queue;
    private int head;
    private int tail;

    // Number of elements in this queue
    private int elementCount;

    public CircularQueue(int length) {
        queue = new int[length];
        head = 0;
        tail = -1;
        elementCount = 0;
    }

    public void insert(int element) {
        // Check the tail index already exceed the max length or not
        if (tail == queue.length - 1) {
            tail = -1;
        }
        tail++;
        queue[tail] = element;
        elementCount++;

        if (elementCount > queue.length) {
            elementCount = queue.length;
        }
    }

    public int remove() {
        if (elementCount == 0) {
            return 0;
        }
        int temp = queue[head];
        queue[head] = 0;
        // Check the head index already exceed the max length or not
        if (head == queue.length - 1) {
            /*
             * If the removed node is tail, it means that the next node will be removed must be the
             * head node since this is a circular queue, so reset head index to 0.
             */
            head = 0;
        } else {
            head++;
        }
        elementCount--;
        return temp;
    }

    public int peek() {
        return queue[head];
    }

    public boolean isEmpty() {
        return elementCount == 0;
    }

    public boolean isFull() {
        return elementCount == queue.length;
    }

    public int getElementCount() {
        return elementCount;
    }

}

```



