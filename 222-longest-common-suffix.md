# Find Longest Common Suffix

定義: 找出兩字串中的最長共同suffix

情境:

* String 1: Cornfield, String 2: outfield 
  -&gt; LCS: field
* String1: Manhours, String 2: manhole 
  -&gt; LCS: NULL \(anho不是suffix\)

這種問題基本上就是要用dynamic programming去解的, 如果以表格來分析的話基本上會長得像下面這張圖:

![](/assets/find_longest_common_suffix.png)

以下是程式的部分:

```java
package idv.carl.leetcode.algorithms.medium.longestcommonsuffix;

/**
 * @author Carl Lu
 */
public class FindLongestCommonSuffix {

    /*
     * This is solved by dynamic programming.
     */
    public static String findLongestCommonSuffix(String str1, String str2) {
        StringBuilder result = new StringBuilder();

        if (isValidString(str1) && isValidString(str2)) {
            int[][] num = new int[str1.length()][str2.length()];
            int maxLength = 0;
            int lastSubStringBegin = 0;

            for (int i = 0; i < str1.length(); i++) {
                for (int j = 0; j < str2.length(); j++) {
                    // If the chars matched
                    if (str1.charAt(i) == str2.charAt(j)) {
                        if ((i == 0) || (j == 0)) {
                            num[i][j] = 1;
                        } else {
                            num[i][j] = 1 + num[i - 1][j - 1];
                        }

                        if (num[i][j] > maxLength) {
                            // Reset the max length if the new ont is grater than the old one
                            maxLength = num[i][j];
                            int currentSubStringBegin = i - num[i][j] + 1;
                            /*
                             * If the new detected substring is derived from the last result,
                             * just append the char to the last result
                             */
                            if (lastSubStringBegin == currentSubStringBegin) {
                                result.append(str1.charAt(i));
                            } else {
                                /*
                                 * However, if the new detected substring is derived from the new
                                 * start point, the result should be updated
                                 */
                                lastSubStringBegin = currentSubStringBegin;
                                result = new StringBuilder();
                                result.append(str1.substring(lastSubStringBegin, i + 1));
                            }
                        }
                    }
                }
            }

            String resultStr = result.toString();
            if (resultStr.length() == 0 || !isSuffix(resultStr, str1, str2)) {
                return "NULL";
            } else {
                return resultStr;
            }

        } else {
            return "NULL";
        }
    }

    private static boolean isValidString(String input) {
        return !(input == null || input.isEmpty());
    }

    // To ensure the result is the common suffix
    private static boolean isSuffix(String result, String str1, String str2) {
        boolean isSuffix = false;
        int lengthOfResult = result.length();

        String str1Sub = str1.substring(str1.length() - lengthOfResult);
        String str2Sub = str2.substring(str2.length() - lengthOfResult);

        if (str1Sub.equals(str2Sub)) {
            isSuffix = true;
        }

        return isSuffix;
    }
}

```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/leetcode/algorithms/medium/longestcommonsuffix/FindLongestCommonSuffix.java)

測試的部分:

```java
package idv.carl.leetcode.algorithms.medium.longestcommonsuffix;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

/**
 * @author Carl Lu
 */
public class FindLongestCommonSuffixTest {

    @Test
    public void testForNormalCase() {
        assertEquals("field", FindLongestCommonSuffix.findLongestCommonSuffix("Cornfield", "outfield"));
    }

    @Test
    public void testForNullCase() {
        assertEquals("NULL", FindLongestCommonSuffix.findLongestCommonSuffix("Manhours", "manhole"));
    }

    @Test
    public void testForInvalidInputCase() {
        assertEquals("NULL", FindLongestCommonSuffix.findLongestCommonSuffix(null, "outfield"));
        assertEquals("NULL", FindLongestCommonSuffix.findLongestCommonSuffix(null, null));
        assertEquals("NULL", FindLongestCommonSuffix.findLongestCommonSuffix("", ""));
        assertEquals("NULL", FindLongestCommonSuffix.findLongestCommonSuffix("", null));
    }

}
```

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/test/java/idv/carl/leetcode/algorithms/medium/longestcommonsuffix/FindLongestCommonSuffixTest.java)

