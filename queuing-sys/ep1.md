# Performance queuing system

## 前言：

香港人煙稠密，很多時你有錢，也未必可以買到你需要的東西。*（圖：口罩）*

所以當一些公司擁有一些稀有資源時，通常都會實施派籌的人流管理措施。一些比較有資源的公司會選擇用網上的派籌/排隊系统，但很可惜有時這些系统有時侯會出一些問題：例如系统負載過量導致死server，或者更嚴重的被[黑客攻擊]。

所以想同大家分折一下一個安全、穩定又可以處理高負載的排隊系统要具備甚麼條件，結構又包括甚麼組成部分?

## 問題根源：

一個正常的網上應用(Web Application)通常都會有Client, Server, Database 三部分，名為 3 tier Architecture. ![3 tier graph]

當大多 client 想同時間 access 一個 server 的時侯，問題就會出現以下兩種情況：

1. Network congestion
1. Server overloaded

簡單來說第一種情況是由於你的連線 bandwidth 不夠高，亦即你駁出街條寬頻唔夠寬，以現今香港的網絡基建，其實很多公司或者data center都會配備光纖網絡，所以好多時問題出現係第二個情況。

這個情況主要原因是 server 的處理運算能力不足以處理短時間大量的請求。其實每一部電腦都有一個極限，小如你的智能手錶、手機、laptop都有，位於data center 的 server 也不例外。

## 解決方法

兩個方向：
1. 控制人流
    1. 分時段：例子：大學 reg course 
    2. Virtural waiting room: 外國公司 [Queue it], 原理就好似一個排隊系統，將你放入一個等候室，好讓目標 server 可以分階段處理你的 requset。分別就係現實世界排隊你要個人企係度，現在可以換部電腦幫你企。
1. 增加處理能力
    1. Load Balancing: 一部唔夠，分開幾部一齊做。
    2. Dynamic Scaling: 好多雲端系统都可以，基本上就係有需要時才出分身處理，無需要時就保持一個低用量模式。

兩個方法各有好壞，第一個方法好處是你不用增加目標 server 的處理能力，就可以處理用戶的大量需求，壞處當然就是用戶需要等。
第二個方法可以減少用戶等待的時間，但壞處就係你很難預算到 server 的支出，因為越多分身，Could service provider, 無論係Google or Amazon，都會同你分身家。

當然，這只是一個很粗淺的解說，實際於做一個 technical decision 時要面對的問題還有很多，例如：
1. 每個request 需要的處理資源有多少
2. 實際樽頸位在那裡

有興趣了解更多的朋友，歡迎留言。



[黑客攻擊]:https://inews.hket.com/article/2588220/%E3%80%90%E6%96%B0%E5%86%A0%E8%82%BA%E7%82%8E%E3%80%91%E5%8F%A3%E7%BD%A9%E5%B7%A5%E5%BB%A0%E9%81%AD%E9%BB%91%E5%AE%A2%E6%94%BB%E6%93%8A%E3%80%80%E6%8E%92%E9%9A%8A%E7%B3%BB%E7%B5%B1Queue-it%E5%87%BA%E6%89%8B%E6%89%93%E6%95%91?mtc=20040
[3 tier graph]:http://tutorials.jenkov.com/images/software-architecture/n-tier-architecture-1.png
[Queue it]:https://queue-it.com/videos/virtual-waiting-room-experience/