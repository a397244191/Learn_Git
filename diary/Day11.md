# Day11
合併、衝突、解決

## merge
我們常常會需要創建分支來幫助我們解決一些問題或是新增一些內容，也暫時不會影響到原本的狀態。但這些總是暫時的，我們會需要跟原本狀態做結合，成為最新的版本，這時後就需要去merge它們。

## 成功的合併
當你merge時，git會將你兩份分支合併起來，即使有相同檔案被修改了，只要修改的地方不一樣，就不會產生衝突。而以下是練習合併的過程。

### 建立被合併的分支

![](https://i.imgur.com/XoXfnKj.png)

如圖，`git checkout -b another`建立並切換到another上，並在裡面為了merge而新增了merge.txt的檔案。並`git commit`來建立版本。

### 合併開始
就像乘法有被乘數跟乘數，雖然交換後結果一樣，但還是有不同名稱。而因為我們要合併回master上，所以我們先切換回master。

![](https://i.imgur.com/QRbmkU6.png)

切換後，為了讓master也產生新版本，所以替master修改了good.txt來創造一個版本。之後用`git merge [branchName]`，因為是合併到此版本，所以只要寫合併過來的分支名稱就好。

### 查看結果

![](https://i.imgur.com/2mEISWd.png)

這裡就能看到，用`git log`，可以看到現在在一個新版本，而去查看這版本可以看到有兩個parent，第一個就是master版本，第二個是another版本。

## 刪除分支
當你認為該分支的工作已經結束了的時候，就會想要刪除不必要的分支，而這時就用`git branch -d [branchName]`來刪除已被合併的分支。但如果我們的分支沒有被合併，可能是發現修改方向完全錯誤之類的，就會用`git branch -D [branchName]`來強行刪除。

### 誤刪啦
當你誤刪分支時該如何處理呢?就是想辦法找回當時得狀況啦!我們用`git reflog`來查看。

![](https://i.imgur.com/odWiZLv.png)

這時可以看到dcae829是當時還未合併前的another分支 ~~(殘骸?)~~ ，記著絕對名稱，我們用`git branch [branchName] [commitID]`來把它變成一個分支，這時後我們剛剛刪除的another 就又回來了。

## 衝突發生
用個簡單的例子來做出衝突的合併。

### 衝突檔案創造
我們切換上剛剛的another，修改了good.txt。

### 合併衝突
我們回到master後合併，這時發生了狀況。

![](https://i.imgur.com/8M1Bkd4.png)

除了合併後的訊息跳出了conflict，查看status可以看到`both modified`表示兩邊都被修改了。用`git diff`可以看到，我們的good.txt變成綠色字樣，而去`type good.txt`，查看內容，good.txt的內容也變成diff的結果。

### 解決方法
當然，這時後用`git add .`直接將狀況變成一個版本當然可以。但是檔案變成這樣大概也不能用了，除此之外，如果跟他人一起共用，隊友有會罵翻你吧。所以我們要來解決這衝突。

![](https://i.imgur.com/tIMJmxp.png)

我們將good.txt自行改成一個新的狀況，並且用`git add .`和`git commit`做成一個新版本。

### 查看修改狀況
我們用`git log`跟`git cat-file -p`來查看一下。

![](https://i.imgur.com/9JAB6DU.png)

可以看出，我們最新版本被當作merge的結果版本，而去檢查內容也能看到兩個parent，表示這是被合併出來的版本，而裡面的第一個是master剛成功合併的版本，而第二個是剛分出去用來產生衝突的分支another。

## 分支樹
內容中提到一些茶看狀態的方法跟解決衝突的方式是用SourceTree，可是我不知道為什麼我的SourceTree安裝上一值卡在半途，今天終於受不了了 ~~(因為是卡住，解決方法不明)~~ 我就去google查看樹的方式。找到了一個指令。

`git log --graph --decorate --oneline --simplify-by-decoration --all`

可以看到現在樹狀態如下圖。

![](https://i.imgur.com/awY74QA.png)

## 感想
除了學會更多merge的不同之處外，也解決了分支樹的查看問題。算是一大收穫。