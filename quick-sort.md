# Quick Sork\(快速排序\)

思想:先根據樞紐值\(pivot\)將資料序列分成兩個子序列, 使左邊序列的所有值都小於pivot, 且右邊都大於pivot, 然後採用同樣的方法來對每個子序列進行快速排序, 最後得到排好順序的資料.

1. 快速排序的重點之一, 就在於選取合理的pivot, 也就是通過pivot來把整個資料序列分成兩個序列.

2. 目前常用的方式是"三資料項取中", 即對資料的第一個, 中間一個及最後一個位置的資料, 找到這三者的中間項.  
   譬如說: 第一個為1, 中間為19, 最後一個為7, 故取三者的中間\(1, 7, 19\)的話, 即為7.

3. 另一個重點, 就在於把資料把資料分成兩個序列, 且要滿足條件\(左邊小於pivot, 右邊大於pivot\).

4. 時間複雜度為: O\(nlogn\)

```java
package idv.carl.sorting;

import java.util.Arrays;

/**
 * @author Carl Lu
 */
public class QuickSort2 {

    public static void main(String args[]) {
        QuickSort2 quickSort = new QuickSort2();
        int[] input = new int[] {3, 5, 4, 8, 7, 90, 80, 88};
        quickSort.quickSort(input, 0, input.length - 1);
        Arrays.stream(input).forEach(data -> System.out.print(data + " "));
    }

    // Here we just take the left node as pivot
    public void quickSort(int[] data, int left, int right) {
        if (left < right) {
            int leftIndex = left;
            int rightIndex = right + 1;

            while (true) {
                while ((leftIndex + 1) < data.length && data[++leftIndex] < data[left]);

                while ((rightIndex - 1) > -1 && data[--rightIndex] > data[left]);

                if (leftIndex >= rightIndex) {
                    break;
                }

                swap(data, leftIndex, rightIndex);
            }

            swap(data, left, rightIndex);
            quickSort(data, left, rightIndex - 1);
            quickSort(data, rightIndex + 1, right);
        }
    }

    private void swap(int[] data, int pos1, int pos2) {
        int tmp = data[pos1];
        data[pos1] = data[pos2];
        data[pos2] = tmp;
    }

}

```


