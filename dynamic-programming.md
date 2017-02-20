# Dynamic Programming \(動態規劃\)

要確認一個問題是否可以用動態規劃去解, 首先要確認是否有以下兩點特性:

1. 重疊子問題 \(Overlapping Sub-problems\)
2. 最佳子結構 \(Optimal Substructure\)

重疊子問題: 即出現需要重複解同樣的子問題的情境. 在遞迴中, 我們每次都要去重解這些子問題, 不過在動態規劃中, 我們只需要去解一次並且將各個子問題的解儲存起來以供將來使用即可. 比較明顯的案例大概就是Fibonacci數列了.

![](/assets/Fibonacci.png)

最佳子結構:

