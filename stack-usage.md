# Stack: Revert String

產生反序的字串  
接續前一章中的自製Stack資料結構, 我們可用此資料結構來做出顛倒字串的動作:

原始碼[點我](https://github.com/yotsuba1022/LeetCode/blob/master/src/main/java/idv/carl/datastructures/stack/ReverseString.java)

```java
package idv.carl.datastructures.stack;

/**
 * @author Carl Lu
 */
public class ReverseString {

    public String doRevert(String input) {
        StringBuffer result = new StringBuffer();
        Stack stack = new Stack(100);

        // Step1. Read the string as chars one by one
        char[] chars = input.toCharArray();

        // Step2. Push those chars into the stack sequentially
        for (char c : chars) {
            stack.push(c);
        }
        
        // Step3. Pop all chars to form a new string
        while (!stack.isEmpty()) {
            result.append((char) stack.pop());
        }

        return result.toString();
    }

}
```



