# Queue\(佇列\)

什麼是Queue: Queue是一種特殊的線性表, 限定只能在表的一端進行插入\(隊尾\), 而在另一端進行刪除操作\(隊頭\), 特點是"先進先出"\(FIFO\).

Queue的基本操作:

1. insert:在隊尾插入資料
2. remove: 從隊頭移走資料
3. peek: 查看隊頭的資料

Circular Queue: 為了避免queue未滿, 卻不能插入新資料項的問題, 可以讓隊頭隊尾的指標繞回陣列開始的位置, 這就是circular queue, 又稱作ring buffer.

Queue的效能: insert和remove的時間複雜度均為O\(1\)

