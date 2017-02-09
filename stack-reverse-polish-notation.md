# Stack: Reverse Polish Notation

計算算式表達式  
後綴表示法: 又稱為[逆波蘭表示法](https://zh.wikipedia.org/wiki/%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E7%A4%BA%E6%B3%95), 此種表示法將運算符寫在運算物件的後面, 例如, 把a+b寫成ab+. 此種表示法的優點是根據運算物件和運算符的出現次序進行運算, 不需要使用括號, 也便於用程式來實作求值.

如何把中綴表達式轉換成後綴表達式:  
把中綴表達式換成後綴表達式不用做算術運算, 只是把操作符和操作數重新按照後綴表達式的方式進行排列而已.

1. 由左至右讀取表達式中的字元
2. 若為操作數, 則複製到後綴表達式字串中
3. 若為左括號, 則push至stack中
4. 若為右括號, 從stack中pop字元至後綴表達式, 直到遇到左括號, 然後把左括號pop出來
5. 若是操作符, 且若此時stack top的操作符優先級≥此操作符, 彈出stack top的操作符到後綴表達式, 直到發現優先級更低的元素位置, 把操作符push至stack
6. 讀到輸入的尾端, 將stack元素pop出來直到該stack為empty, 將符號寫入後綴表達式中

```java
package idv.carl.datastructures.stack;

/**
 * @author Carl Lu
 */
public class ReversePolishNotation {

    private final static int PRIORITY_LEVEL_1 = 1;
    private final static int PRIORITY_LEVEL_2 = 2;
    private final static char ADD = '+';
    private final static char MINUS = '-';
    private final static char MULTIPLY = '*';
    private final static char DIVIDE = '/';
    private final static char LEFT_PARENTHESES = '(';
    private final static char RIGHT_PARENTHESES = ')';

    public String doTransfer(String input) {
        StringBuffer result = new StringBuffer();
        Stack stack = new Stack(50);
        // Step1. Transform the input into char array
        char[] chars = input.toCharArray();
        // Step2. Apply related operation rule on each char
        for (int i = 0; i < chars.length; i++) {
            char c = chars[i];

            // 2.1 If it's operator, operate it according to the priority
            if (isAddOrMinus(c)) {
                doOperation(stack, result, c, PRIORITY_LEVEL_1);
            } else if (isMultiplyOrDivide(c)) {
                doOperation(stack, result, c, PRIORITY_LEVEL_2);
            }
            // 2.2 If it's left bracket, push to stack
            else if (c == LEFT_PARENTHESES) {
                stack.push(c);
            }
            // 2.3 If it's right bracket, pop from stack, stop when encounter the left bracket
            else if (c == RIGHT_PARENTHESES) {
                handleForRightBracket(stack, result);
            }
            // 2.4 If it's operand, add to output directly
            else {
                result.append(c);
            }
        }

        // Step3. If iterate to the end, pop up the operator into the output
        while (!stack.isEmpty()) {
            result.append((char) stack.pop());
        }
        return result.toString();
    }

    private void handleForRightBracket(Stack stack, StringBuffer result) {
        // Step1. Pop up value from stack into result
        while (!stack.isEmpty()) {
            char top = (char) stack.pop();
            // Step2. Stop until meet the left bracket
            if (top == LEFT_PARENTHESES) {
                break;
            } else {
                result.append(top);
            }
        }
    }

    private boolean isAddOrMinus(char c) {
        return (c == ADD || c == MINUS);
    }

    private boolean isMultiplyOrDivide(char c) {
        return (c == MULTIPLY || c == DIVIDE);
    }

    private void doOperation(Stack stack, StringBuffer result, char c, int priority) {
        // Step1. Obtain value from the top of stack
        while (!stack.isEmpty()) {
            char top = (char) stack.pop();
            // Step2. Compare with input char according to priority
            // 2.1 If top is left bracket, do nothing (need to push back the value)
            if (top == LEFT_PARENTHESES) {
                stack.push(top);
                break;
            } else {
                // Determine the priority of the top element
                int pTop;
                if (isAddOrMinus(c)) {
                    pTop = PRIORITY_LEVEL_1;
                } else {
                    pTop = PRIORITY_LEVEL_2;
                }

                if (pTop >= priority) {
                    // 2.2 If p(top) ≥ p(value), add top to result
                    result.append(top);
                } else {
                    // 2.3 If p(top) < p(value), do nothing (need to push back the value)
                    stack.push(c);
                    break;
                }
            }
        }
        // Step3. After found the lower priority element, push into the stack
        stack.push(c);
    }

}

```









