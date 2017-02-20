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
    public static long fibonacci(int n) {
        if (n <= 1) {
            return n;
        } else {
            return fibonacci(n - 1) + fibonacci(n - 2);
        }
    }
```

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
    public static long findFibonacciWithDynamicProgramming(int n) {
        long fib[] = new long[n + 1];
        fib[0] = 1l;
        fib[1] = 1l;

        for (int i = 0; i <= n; i++) {
            if (i <= 1) {
                System.out.println("Fibonacci " + i + ": " + fib[i]);
            } else {
                fib[i] = fib[i - 1] + fib[i - 2];
                System.out.println("Fibonacci " + i + ": " + fib[i]);
            }
        }

        return fib[n];
    }
```



