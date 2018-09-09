# Day16
三日不讀書，便覺面目可憎。為了不讓自己之後見人呈現難看臉給對方，當天再有事也要盡量維持看些東西的好習慣 ~~(當然因為太累或太晚，偷斤減兩跟偷懶一天是可以容忍的，畢竟我之前就偷懶過了，呵呵)~~

## revert and cherry-pick
這不是因為之前提到的東西有什麼需要補充的。而是提及一下，之前做的有點像是套用舊的commit並merge到現在版本的感覺。而今天要提及的，有些類似有些不同。

## rebase
`git rebase [commitID]`，其中commit常常用branch代替，因為是說將某些分支內容設定為現在分支的基礎，就是說，假設分支有master跟branch1各有修改，想讓branch1的修改建立在master上，就在branch1的分支上執行`git rebase master`，此時master和branch1的分岔點就變成現在的master，而因為master還未更新，所以最新的版本是branch1。如下圖變化。

![](https://i.imgur.com/eXMIX9d.png)

master成為branch1的基底，branch1是由master後修改而成的。常常會用到於一些分支要建立前後基礎關係時的時機。

### merge快轉機制
原始分支：

![](https://i.imgur.com/rOHMNHI.png)

上為經由快轉機制的，而下沒有。

![](https://i.imgur.com/YIF3e2T.png)

其中差別在於`--no-ff`參數的差別，而內容則是差在沒有快速轉換，會建立一個版本當作merge後的狀態。

而這時候可以看出來master跟branch1的分支點從原來的"a.txt is 2"變成了"a.txt is 3"，這樣會比一般merge在觀感上更線性。

![](https://i.imgur.com/yVH2Gm4.png)

這是之前merge的狀態，在這裡我們只能感覺到4bdd跟6368的時間關係，卻無法得知他們內容上的先後。而經過rebase後，可以讓人感受出一種，A功能完成是基於B功能的完成而完成的，聽起來饒舌，但也有助於開發上跟建立版本上的差異。

## 衝突
因為之前版本都是建立在最新版本上，而這次的作法是把commit移至現有commit狀態下，所以想試試看衝突的狀況。起初雖然製造出衝突了，但是不知道是用commit還是什麼，所以嘗試了一下出現這樣的狀況。

![](https://i.imgur.com/hqFRsVy.png)

此圖為衝突發生狀況。

![](https://i.imgur.com/qUJmA6N.png)

此時用`git branch`可以看出我們現在多了一個暫時的branch儲存當前狀況，而修改過後，我很天真的以為用`git commit`可以解決，因為以前沒提及的，`git commit`就能製造最新版本，所以認為是對的，但這次無法偷吃步了，因為版本樹狀圖可以明顯感受出沒有rebase。

### 解決衝突
經過一番google後，發現跟resert一樣，是用`--continue`來解決。

![](https://i.imgur.com/wA60VWA.png)

所以這是解決後的狀態。是真的rebase後的呢。

### cherry-pick衝突
因為cherry-pick沒有衝突例子，所以我從那時就沒有舉一反三的想法認為`--continue`才是正確的。如今遇到正式狀況，還是來好好練習吧。

![](https://i.imgur.com/oazS8Tz.png)

我隨手撿了一個舊時候的更正，用`--continue`解決了衝突問題。

## 感想
做完這個練習後，雖然可以說我知道怎麼用rebase，但對於使用情境並非十分了解，大概只有之後實際遇到才會懂得那感覺吧。

並且在這次注意到之前未注意的問題跟解決法，也算是一個收穫。