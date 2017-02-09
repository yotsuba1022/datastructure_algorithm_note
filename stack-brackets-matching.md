# Stack: Brackets Matching

當想要檢驗一個輸入當中的括號順序跟種類是否正確, 可以透過stack來做檢查.

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/datastructures/stack/CheckBrackets.java)

```java
package idv.carl.datastructures.stack;

/**
 * @author Carl Lu
 */
public class CheckBrackets {

    private final static char FORMER_PARENTHESES = '(';
    private final static char LATTER_PARENTHESES = ')';
    private final static char FORMER_BRACKET = '[';
    private final static char LATTER_BRACKET = ']';
    private final static char FORMER_BRACE = '{';
    private final static char LATTER_BRACE = '}';

    public boolean check(String input) {
        boolean match = true;
        Stack stack = new Stack(50);
        // Step1. Transform the string into char array
        char[] chars = input.toCharArray();

        for (int i = 0; i < chars.length; i++) {
            char c = chars[i];

            if (isFormerPart(c)) {
                /*
                 * Step2. Read chars sequentially, push the char into stack
                 * if it's the former part of the brackets
                 */
                stack.push(c);
            } else if (isLatterPart(c)) {
                /*
                 * Step3. If encounter the latter part of the brackets,
                 * pop a value from stack and try to match
                 */
                char former = (char) stack.pop();
                if (misMatch(former, c)) {
                    System.out.println("Char mismatch, index at: " + (i + 1));
                    match = false;
                } else {
                    System.out.println("Char match.");
                    match = true;
                }
            }

        }
        return match;
    }

    private boolean isFormerPart(char c) {
        return (c == FORMER_PARENTHESES || c == FORMER_BRACKET || c == FORMER_BRACE);
    }

    private boolean isLatterPart(char c) {
        return (c == LATTER_PARENTHESES || c == LATTER_BRACKET || c == LATTER_BRACE);
    }

    private boolean misMatch(char former, char latter) {
        return ((former == FORMER_PARENTHESES && latter != LATTER_PARENTHESES)
                || (former == FORMER_BRACKET && latter != LATTER_BRACKET) || (former == FORMER_BRACE && latter != LATTER_BRACE));
    }

}
```



