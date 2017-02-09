# Stack\(堆疊\)

線性表:

又稱為順序表, 是一個線性的序列結構, 是一個含有n≥0個節點的有線序列, 對於其中的節點:

1. 有且僅有一個開始節點, 沒有前驅, 但有後繼節點
2. 有且僅有一個終端節點, 沒有後繼, 但有前驅節點
3. 其他的節點都有且僅有一個前驅和後繼節點
4. [維基百科](https://zh.wikipedia.org/wiki/%E7%BA%BF%E6%80%A7%E8%A1%A8)

線性表跟陣列的比較:

1. 是兩種不同的資料結構, 陣列有維度的概念, 線性表沒有; 線性表有前驅/後繼節點的概念, 且線性表的資料是相互有關聯的, 但陣列並沒有這些概念.
2. 線性表可以使用陣列來實作, 通常用一維陣列來作為其資料的存儲結構.

什麼是Stack\(堆疊\):

1. Stack是一種特殊的線性表, 限定只能在表的一端進行插入和刪除操作, 俗稱後進先出\(LIFO\).
2. 操作資料的這一端就稱為表頭, 或top, 相對地, 另一端叫bottom, 不含任何元素的時候叫做empty stack.

Stackk的基本操作:

1. push: 塞東西到stack
2. pop: 把最上面的東西彈出來
3. peek: 只觀看最上面的東西, 不要彈出來

```java
package idv.carl.datastructures.stack;

/**
 * @author Carl Lu
 */
public class Stack {

    private int[] data;
    private int top = -1;

    public Stack(int length) {
        data = new int[length];
    }

    public void push(int element) {
        if (top < this.data.length - 1) {
            top++;
            this.data[top] = element;
        }
    }

    public int pop() {
        return data[top--];
    }

    public int peek() {
        return data[top];
    }

    public boolean isEmpty() {
        return top == -1;
    }

    public boolean isFull() {
        return top == data.length - 1;
    }

    public int size() {
        return top + 1;
    }

}

```



