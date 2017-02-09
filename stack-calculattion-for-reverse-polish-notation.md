# Stack: Calculation for Reverse Polish Notation

計算後綴表達式求值

1. 從左到右依序讀取表達式中的字元
2. 若是運算元, push to stack
3. 若是運算子, 從stack中pop出兩個資料進行運算, 並把結果push入stack中
4. 直到表達式結束 



