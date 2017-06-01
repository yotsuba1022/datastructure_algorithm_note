# Fibonacci Series \(斐波那契數列\)

關於Fibonacci series的定義如下:

![](/assets/Fibonacci2.png)

其在數學上是以**遞迴**的方式定義的.

以下就簡單列出遞迴解法跟動態規劃解法

### 遞迴:

```java
    /*
     * Recursive solution.
     *
     * This solution cannot solve big input.
     * You can found that it will go very slowly after n ≥ 35
     *
     * Time Complexity: O(2^n)
     */
    public static long findFibonacci(int n) {
        long result = 0;

        for (int i = 1; i <= n; i++) {
            if (n <= 1) {
                result = n;
            } else {
                result = findFibonacci(n - 1) + findFibonacci(n - 2);
            }
        }

        return result;
    }
```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/leetcode/algorithms/easy/fibonacci/FibonacciRecursive.java)

### 動態規劃:

```java
    /*
     * Dynamic Programming — Memoization
     * (Bottom-Up Approach)
     * 
     * Store the sub-problems result so that you don’t have to calculate again.
     * So first check if solution is already available,
     * if yes then use it else calculate and store it for future.
     *
     * Time Complexity: O(n) , Space Complexity : O(n)
     */
    public static long findFibonacci(int n) {
        long fib[] = new long[n + 1];

        fib[0] = 0l;
        fib[1] = 1l;

        for (int i = 0; i <= n; i++) {
            if (i > 1) {
                fib[i] = fib[i - 1] + fib[i - 2];
            }
        }

        return fib[n];
    }
```

Python版本:

```py
def fibonacci(n):
    
    a = 1
    b = 1
    
    for i in range(n):
        yield a
        a, b = b, a + b
```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/leetcode/algorithms/easy/fibonacci/FibonacciDynamicProgramming.java)

測試程式:

```java
package idv.carl.leetcode.algorithms.easy.fibonacci;

import static org.junit.Assert.assertEquals;

import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.Timeout;

/**
 * @author Carl Lu
 */
public class FibonacciTest {

    @Rule
    public Timeout timeout = Timeout.seconds(3);

    @Test
    public void testForRecursiveWay() {
        assertEquals(55, FibonacciRecursive.findFibonacci(10));
    }

    @Test
    public void testForDynamicProgrammingWay() {
        assertEquals(55, FibonacciDynamicProgramming.findFibonacci(10));
    }

    /*
     * This will failed.
     */
    @Test
    public void testTimeoutForRecursiveWay() {
        assertEquals(12586269025L, FibonacciRecursive.findFibonacci(50));
    }

    @Test
    public void testTimeoutForDynamicProgrammingWay() {
        assertEquals(12586269025L, FibonacciDynamicProgramming.findFibonacci(50));
    }

    @Test
    public void testTimeoutForDynamicProgrammingWay2() {
        assertEquals(7540113804746346429L, FibonacciDynamicProgramming.findFibonacci(92));
    }

}
```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/test/java/idv/carl/leetcode/algorithms/easy/fibonacci/FibonacciTest.java)

