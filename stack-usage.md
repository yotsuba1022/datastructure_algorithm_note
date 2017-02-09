# Stack的應用

1. 產生反序的字串  
   接續前一章中的自製Stack資料結構, 我們可用此資料結構來做出顛倒字串的動作:

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

2. 括號\(brackets\)的匹配

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

3. 計算算式表達式  
   後綴表示法: 又稱為逆波蘭表示法, 此種表示法將運算符寫在運算物件的後面, 例如, 把a+b寫成ab+. 此種表示法的優點是根據運算物件和運算符的出現次序



