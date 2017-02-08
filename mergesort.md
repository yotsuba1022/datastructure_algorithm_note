Merge Sort\(合併排序\)

思想: 採用Divide and Conquer的做法, 將資料序列分成兩個子序列, 排序每一半, 然後再把排序好的兩個子序列合併成為一個有序的序列.

效率: Merge Sort的時間複雜度是O\(nlogn\), 主要是複製跟比較會花比較多時間

```java
package idv.carl.sorting;

import java.util.Arrays;

/**
 * @author Carl Lu
 */
public class MergeSort {

    public static void main(String args[]) {
        MergeSort mergeSort = new MergeSort();
        int[] input = new int[] {4, 8, 10, 1, 5, 9, 7};
        mergeSort.mergeSort(input);
        Arrays.stream(input).forEach(data -> System.out.print(data + " "));
    }

    public void mergeSort(int[] data) {
        int[] temp = new int[data.length];
        doMergeSort(data, temp, 0, data.length - 1);
    }

    private void doMergeSort(int[] data, int[] temp, int from, int to) {
        if (from >= to) {
            return;
        }
        // Step1. Calculate the bound index
        int mid = (from + to) >> 1;
        // Step2. Sort the left part
        doMergeSort(data, temp, from, mid);
        // Step3. Sort the right part
        doMergeSort(data, temp, mid + 1, to);
        // Step4. Merge the two parts
        merge(data, temp, from, mid + 1, to);
    }

    private void merge(int[] data, int[] temp, int from, int mid, int to) {
        // The index for merged data in temp array
        int count = 0;
        // The min index of the left part
        int minLeft = from;
        // The max index of the left part
        int maxLeft = mid - 1;

        // Step1. Get values from left part and compare with the right part
        while (from <= maxLeft && mid <= to) {
            if (data[from] < data[mid]) {
                // If left < right, add the left value into temp
                temp[count++] = data[from++];
            } else {
                // If left > right, add the right value into temp
                temp[count++] = data[mid++];
            }
        }

        // Step2. Handle the remaining part:
        // 2.1 For the left part
        while (from <= maxLeft) {
            temp[count++] = data[from++];
        }
        // 2.2 For the right part
        while (mid <= to) {
            temp[count++] = data[mid++];
        }

        // Step3. Copy the final results from temp array into data array
        for (int i = 0; i < (to - minLeft + 1); i++) {
            data[minLeft + i] = temp[i];
        }
    }

}

```



