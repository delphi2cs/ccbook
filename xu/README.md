# 序

此線上電子書還在寫作中，仍未完成。[回饋給作者](https://goo.gl/forms/DWmgm5fChpJ6IEFI3)

對於想塞進一本書的分量來說，這本書所涵蓋的範圍是稍嫌貪心的。本書開發的是把C語言的程式碼轉（source code）換成組合語言（assembly code）用的程式，也就是所謂的C編譯器。而這個編譯器本身也是以C語言所開發。現階段的目標是Self-hosting－也就是自幹的編譯器要可以編譯其自己的程式碼。

本書為了避免解釋編譯器的難度突然上升太快，會以各式各樣的主題貫穿全書，漸漸加深難度的方式來進行。理由如下：

編譯器的概念可以分為幾個階段：語法分析、中途傳遞和產出指令。常見的教科書會以這些階段各自做為一個主題介紹，但是這樣的作法很容易在途中特定主題顯得過度深入，讓讀者難以跟上。

此外，分階段開發的作法在沒有完成所有階段之前，編譯器是沒辦法完整運作的，就算讀者的理解或是程式碼有關鍵的錯誤，很可能直到完整運作之前讀者都不會發現。而且說實話，對於下一個階段想要什麼樣的輸入，在自己開發到下一個階段之前其實也搞不太清楚，當然也就搞不太清楚前一個階段的輸出到底該怎麼樣才是對的。更何況在完成編譯器前都沒辦法編譯像樣的程式碼的狀況下，要如何維持開發的熱誠和動力也是一個困難的問題。

本書為了避開這種陷阱採用了不同的方針。在書的最開始，讓讀者實作語法非常單純的「自創語言」。因為該語言真的很單純，實作時並不需要了解編譯器的細節。之後，讀者在閱讀本書的過程中逐漸把功能實作到這個「原創語言」上，最後讓該語言成長到變得與C語言一致。

透過此種漸進式的開發方法，一邊提出一個一個小的commit，一步一步開發編譯器。在這個開發方法底下，每一個小的commit其實都是「完整的」編譯器。也就是說，在某個階段可能只是計算機等級的語言；某個階段可能是一個小範圍C語言的子集合；在某個階段可能就幾乎是完整的C語言了。關鍵在於，配合當時的完成度讓當時的語言有合理的結構，而不是在開發中只讓某部分的功能很突出、很像C語言。

本書所用到的資料結構與演算法、相關的基礎CS知識都會配合開發的進度逐步講解。

在漸進式的開發方法中，讀者在讀本書的任一時間點都會很均衡的對程式語言實作方法有合理的理解。這比起只偏重了解編譯器的特定主題要好得多。最後讀完本書的時候，相信對於所有的主題的知識都會有很均衡的理解了吧。

此外，本書同時也是說明該如何從頭開始寫一個大型程式專案的教學書。明明「製作大型程式」這種技能是和資料結構、演算法等完全不一樣的特技，但卻沒有很多書在介紹。而且就算有講解，沒有實際體驗過的話，也很難真正理解何謂好的和不好的開發方法。本書雖然是講如何讓自己開發的語言成長成C語言的過程，但同時也是設計成一個體驗良好開發方法的機會。

如果筆者的計畫是成功的話，讀者在閱讀本書不只是學習到製作編譯器的技巧或是CPU指令及等的知識，也同時可以學習到一步步小從小的步驟開發大型程式的方法、軟體測試的方法、版本管理的方法，連面對像開發編譯器這種富含野心的計畫時，該做好什麼樣的心理準備都可以一次學到。

本書設想的讀者是普通的C語言程式開發者，讀者不必是很熟悉C語言語法的超級C語言專家。只要可以理解指標、陣列，花上一點時間可以讀得懂別人用C開發的小型程式就沒問題了。

本書中對言語的結構或是CPU的架構等，不會只是說明其結構，也會盡可能介紹為什麼選擇這樣的設計。並且為了讓讀者可以開心地讀下去，花了些許心思加入了可以引起興趣的編譯器、CPU、電腦業界的歷史等的小知識。

開發編譯器是非常開心的事。最初笨笨的，只能做很單純工作的自創言語編譯器，持續開發下去漸漸變得像C語言，連自己都會大吃一驚，而且像魔法一樣暢行無阻。實際開發下去後，常常會因為之前完全不能想像可以編的動的大型測試程式都可以無誤地編譯出來，而且可以完全正確執行而感到驚訝。而看看那些程式碼編譯出來的組合語言指令自己也搞不太懂，有時甚至會覺得編譯器是不是比身為作者的自己還聰明。就算可以搞懂編譯器的原理，編譯器這種程式常常讓人感到「為什麼可以這麼順利運作？」，而有一種無法言喻又不可思議的感覺。相信讀者也可以感受到其中的魅力而為之著迷吧。

前言就講到這邊，大家一起和筆者跳進開發編譯器的世界吧！

{% hint style="info" %}
小知識：為什麼選擇C語言

在許多程式語言中，為什麼本書要選擇C語言呢？又或者自創語言不好嗎？其實，並不是非C語言不可，但是為了以學習產出機械語言編譯器的開發方法來選語言的話，其實合適的選擇並不是那麼多，而筆者認為C語言正是其中之一。

直譯式的程式語言無法學到低階系統運作，而C語言則可以編譯成組合語言，所以在製作C編譯器的同時可以同時學到C語言本身、CPU指令集、還有程式運作的架構。

如果編譯器開發順利的話，C語言的程式非常常見，去網路上下載一些第三方的程式碼來試著編譯也是滿有趣的，像是嘗試編看看迷你Unix核心的xv6。如果編譯器的完成度夠高，理論上連Linux核心都是可以編出來的。這些都是自製語言或是比較冷門的語言沒辦法試的。

此外，開發自製語言雖然有著可以練習語言設計的好處，但其實還是有陷阱。像是實作麻煩的地方就直接在語言規範裡排除掉就解決了，而C語言這種有語言標準規範的語言就不能這樣做。這些限制在學習上還是滿有好處的。
{% endhint %}


