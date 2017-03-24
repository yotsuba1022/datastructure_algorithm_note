# Binary Search

一般來說, binary search是用來在已排序好的集合中搜尋用的方法, 以下是在一個排序好的array中找出指定值的index之做法, 分別為遞迴版跟迴圈版, 時間複雜度為O\(logn\):

```java
package idv.carl.leetcode.algorithms.easy.binarysearchinarray;

/**
 * @author Carl Lu
 */
public class BinarySearch {

    public static int searchRecursively(int[] input, int key, int from, int to) {
        if (from > to) {
            return -1;
        }

        /*
         * int mid = (from + to) >> 1;
         * 
         * It also works, however,
         * except when (from + to) produces int overflow.
         */
        int mid = from + ((to - from) >> 1);

        if (input[mid] > key) {
            return searchRecursively(input, key, from, mid - 1);
        } else if (input[mid] < key) {
            return searchRecursively(input, key, mid + 1, to);
        } else {
            return mid;
        }
    }

    public static int searchIteratively(int[] input, int key) {
        int from = 0;
        int to = input.length - 1;

        while (from <= to) {
            int mid = from + ((to - from) >> 1);
            if (input[mid] > key) {
                to = mid - 1;
            } else if (input[mid] < key) {
                from = mid + 1;
            } else {
                return mid;
            }
        }

        return -1;
    }

}
```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/leetcode/algorithms/easy/binarysearchinarray/BinarySearch.java)

測試程式:

```java
package idv.carl.leetcode.algorithms.easy.binarysearchinarray;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

/**
 * @author Carl Lu
 */
public class BinarySearchTest {

    private static int[] input = new int[] {1, 2, 4, 5, 6, 7, 8, 9, 10, 12};

    @Test
    public void testSearchRecursively() {
        assertEquals(3, BinarySearch.searchRecursively(input, 5, 0, input.length));
    }

    @Test
    public void testSearchRecursivelyIfNoMatching() {
        assertEquals(-1, BinarySearch.searchRecursively(input, 3, 0, input.length));
    }

    @Test
    public void testSearchIteratively() {
        assertEquals(3, BinarySearch.searchIteratively(input, 5));
    }

    @Test
    public void testSearchIterativelyIfNoMatching() {
        assertEquals(-1, BinarySearch.searchIteratively(input, 3));
    }
}
```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/test/java/idv/carl/leetcode/algorithms/easy/binarysearchinarray/BinarySearchTest.java)

遞迴只應天上有, 凡人應當用迴圈 \(嘆\)

