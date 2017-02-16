# Priority Queue {#firstHeading}

Priority Queue: 優先佇列, 即資料按照關鍵字排好的佇列, 詳細可見[維基百科](https://zh.wikipedia.org/wiki/%E5%84%AA%E5%85%88%E4%BD%87%E5%88%97)

Priority Queue的效率: 下方的是比較粗糙的實作, insert需要**O\(n\)**, 而remove是O\(1\), 通常這邊要改進insert的效能可以用**heap tree**來實作內部的資料結構, 這樣可以令insert的效能提升至**O\(logn\), **所以也有人將改進後的priority queue稱為是一種**complete binary tree.**

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/datastructures/queue/PriorityQueue.java)

```java
package idv.carl.datastructures.queue;

/**
 * @author Carl Lu
 */
public class PriorityQueue {

    private int[] queue;

    // Number of elements in this queue
    private int elementCount;

    public PriorityQueue(int length) {
        queue = new int[length];
        elementCount = 0;
    }

    public void insert(int element) {
        if (elementCount == queue.length) {
            return;
        } else if (elementCount == 0) {
            queue[elementCount] = element;
        } else {
            /*
             * If the queue is not empty, execute sorting before insert the element
             */
            int i;
            for (i = elementCount - 1; i >= 0; i--) {
                if (element > queue[i]) {
                    queue[i + 1] = queue[i];
                } else {
                    break;
                }
            }
            queue[i + 1] = element;
        }
        elementCount++;
    }

    public int remove() {
        if (elementCount == 0) {
            return 0;
        }
        // Decrease the elementCount because it already be increased at the end of insert.
        elementCount--;
        // Remove the last element
        int removed = queue[elementCount];
        // Assume that 0 means the data was removed
        queue[elementCount] = 0;
        return removed;
    }

    public int peek() {
        return queue[elementCount - 1];
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



