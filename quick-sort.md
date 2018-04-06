# Quick Sork\(快速排序\)

**思想:先根據樞紐值\(pivot\)將資料序列分成兩個子序列, 使左邊序列的所有值都小於pivot, 且右邊都大於pivot, 然後採用同樣的方法來對每個子序列進行快速排序, 最後得到排好順序的資料.**

1. 快速排序的重點之一, 就在於**選取合理的pivot**, 也就是通過pivot來把整個資料序列分成兩個序列.

2. 目前常用的方式是"三資料項取中\(a.k.a. **Balanced Quick Sort**\)", 即對資料的第一個, 中間一個及最後一個位置的資料, 找到這三者的中間項. 譬如說: 第一個為1, 中間為19, 最後一個為7, 故取三者的中間\(1, 7, 19\)的話, 即為7.

3. 另一個重點, 就在於把資料分成兩個序列, 且要滿足條件\(左邊小於pivot, 右邊大於pivot\).

4. 時間複雜度為: **O\(nlogn\), 最差為O\(n^2\)                                    
   **-&gt; 在partition的部分, 因為要將所有的元素都拿來跟pivot比過一次, 所以迭代所有元素的時間複雜度是O\(n\), 合併雖然會因為實作而異, 但了不起就是O\(n\)了; 因此重點就會是在切割的次數, 畢竟切割次數會被pivot的選擇影響到, 最好的情況下, 就是每次都切割成相同大小的子陣列, 這樣就是切割logn次. 假如運氣太差了, 即每次取pivot都取到該數列的最大或最小值\(碰到完全排好的資料然後你pivot又只抓最右邊或最左邊就會變這樣\), 如此一來, 變成將原本的陣列切成0跟n-1\(不包含pivot\), 這樣就會有n次的遞迴呼叫, 故時間複雜度最佳為O\(nlogn\), 最差為O\(n^2\).

5. 空間複雜度: **最佳為O\(nlogn\), 最差為O\(n^2\)**  
   -&gt; 由於每次都會把資料分成兩份子陣列, 因此會申請兩個新的子陣列記憶體空間, 對每個遞迴來說這部分的空間複雜度就是O\(n\), 而遞迴呼叫的最佳情況為logn次, 最差為n次, 所以空間複雜度的最佳為O\(nlogn\), 最差為O\(n^2\).

6. In-place版本: 這種做法可以讓我們不用為子陣列申請新的記憶體空間, 所以每次遞迴都只需要O\(1\)的空間複雜度\(for swap function\), 而通常此版本的一個特色就是**僅需要做partition的操作, 不必再有merge了, 因為partition的時候也做完merge了**.

以下的範例就是in-place的版本, pivot是直接取中間的元素.

```java
package idv.carl.sorting.quicksort;

/**
 * @author Carl Lu
 */
public class QuickSortByMiddlePivot {

    public static void sort(int[] data) {
        if (data == null || data.length == 0) {
            return;
        }
        quickSort(data, 0, data.length - 1);
    }

    private static void quickSort(int[] data, int leftBound, int rightBound) {
        int left = leftBound;
        int right = rightBound;

        int pivot = data[leftBound + ( rightBound - leftBound ) / 2];

        while (left < right) {
            while (data[left] < pivot) {
                left++;
            }

            while (data[right] > pivot) {
                right--;
            }

            if (left <= right) {
                swap(data, left, right);
                left++;
                right--;
            }
        }

        if (leftBound < right) {
            quickSort(data, leftBound, right);
        }

        if (left < rightBound) {
            quickSort(data, left, rightBound);
        }
    }

    private static void swap(int[] data, int left, int right) {
        int temp = data[left];
        data[left] = data[right];
        data[right] = temp;
    }

}

```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/sorting/quicksort/QuickSortByMiddlePivot.java)



測試程式:

```java
package idv.carl.sorting.quicksort;

import org.junit.Test;

import java.util.Arrays;

import static org.junit.Assert.*;

/**
 * @author Carl Lu
 */
public class QuickSortByMiddlePivotTest {

    @Test
    public void testForNullInput() {
        int[] actual = null;
        QuickSortByMiddlePivot.sort(actual);
        assertNull(actual);
    }

    @Test
    public void testForEmptyInput() {
        int[] actual = new int[] {};
        QuickSortByMiddlePivot.sort(actual);
        assertEquals(0, actual.length);
    }

    @Test
    public void testForNormalCase() {
        int[] actual = new int[] {9, -32, 102, 4, -5, 8, 0, 7, 77, 1, 30};
        int[] expected = new int[] {-32, -5, 0, 1, 4, 7, 8, 9, 30, 77, 102};
        QuickSortByMiddlePivot.sort(actual);
        assertTrue(Arrays.equals(expected, actual));
    }

    @Test
    public void testForDuplicateElement() {
        int[] actual = new int[] {7, 7, 8, 8, 7, 7, 8, 8, 9, 9, -1, -1, 2, 2, 0};
        int[] expected = new int[] {-1, -1, 0, 2, 2, 7, 7, 7, 7, 8, 8, 8, 8, 9, 9};
        QuickSortByMiddlePivot.sort(actual);
        assertTrue(Arrays.equals(expected, actual));
    }

}

```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/test/java/idv/carl/sorting/quicksort/QuickSortByMiddlePivotTest.java)

關於程式的解說, 可以看[這個commit](https://github.com/yotsuba1022/LeetCode/commit/0c4e90866bbafeea9b405c1a039bc5db3e6b9b5a).

