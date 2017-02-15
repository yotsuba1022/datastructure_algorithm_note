# Merge Sort v.s. Quick Sort

* 兩者其實非常相似, 都是把資料分成兩邊, 直到不能再分了, 才把資料合起來. 不過quick sort最大的特色就是會有**partition**的這個動作, 講白了就是**把數字分好大小後再繼續往下分**, 所以這樣循環下去分到最小後, 也表示完成了排序的動作了.

* 在大部分的worst case下, merge sort是優於quick sort的, 再加上merge sort的worst case跟quick sort的bast case之時間複雜度是一樣的, 這樣看來似乎是merge sort比較快\(理論上\).

* 可是實際上來說, 如果兩者都用遞迴的方式去實作的話, quick sort的method call為N, 那merge sort就會是2N-1, 即merge sort多花了一倍的method call. 如果用迴圈來做, merge sort會花比較多時間在記憶體上面, 因為它不是in-place sorting.

* 不過merge sort有一個很好的特性: 它是**穩定**的\(**stable sorting**\), 穩定的意思是說, 排序前與排序後, 擁有相同key值的兩個資料, 彼此之間的順序是一樣的.

* 最後, 這兩者都是Divide and Conquer的做法, 只是**quick sort為先苦後樂**\(遞迴之前的partition比較麻煩, 遞迴完後就沒事了\); 而**merge sort是先樂後苦**\(進入遞迴之前都沒事, 但是遞迴之後的合併動作就累了\).



