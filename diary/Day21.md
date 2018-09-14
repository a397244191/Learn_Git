# Day21
善用分支以利主版本便於管理。

## 初始管理者
我們利用之前開的emptybox的repository來操做一些東西。先clone到一個新資料夾。

![](https://i.imgur.com/ehw66Jz.png)

### 分支
接下來我們來做一些便於管理的分支項目吧。

- `develop`
  - 開發下的分支，各種開發項目都在這分支上。
- `feature/[branchName]`
  - 在develop分支上，另外的分支，為了新增小功能/測式小部件用的。
- `hotfix/[branchName]`
  - 在master上，多是為了緊急修正bug用。

這些是文中提到的一些常見狀況使用的分支類別。

### 標籤
有時候在master穩定更新後，就會需要一些標籤來幫你記錄一些重要版本。

例如:`git tag [version tag name] -a -m "some message"`這類的方式來幫你記錄一些重要版本，而版本名稱可能長這樣`1.0.0-beta1`之類的(就內文用的)。

### 創建並上傳
認識這些後，我們可以預設好一些需要的分支跟標籤後再上傳到遠端。

![](https://i.imgur.com/VYgud4A.png)

上圖依序就是"創建develop"$\rightarrow$"在develop建立feature/aspnet_identity"$\rightarrow$"在master建立hotfix/bugs_in_membership"(圖中打錯字，hotfix後用成''不是'/')$\rightarrow$"建立tag在master上"

之後用`git push -all`上傳所有branch，如果tag也要上傳，要用`git push --tags`。

## 實際操作一些東西
上面這些已經在遠端建立一些需要的東西。接下來我們扮演其它使用者被分配工作的狀況吧。

### User2
我們在不同資料夾上，clone一個版本下來，可以看到。

![](https://i.imgur.com/RF3FYr3.png)

上圖可以看到，我們`git branch -a`可以看到我們剛剛push上去的branch變成遠端分支了。

![](https://i.imgur.com/YuFIPgq.png)

假設，user2被交付的工作是修改當下出現的bug，我們可以利用`git checkout hotfix/bugs_in_membership`來創建本地追蹤分支。修改完後，我們用`git push origin hotfix/bugs_in_membership`將bug修正上傳到遠端，而這分支暫時是沒有merge的，可能是有不同成員一起修正之類的原因。

### User3
我們再次clone一個新資料夾當做第三使用者。這次它可能是要做開發部分的，而這次部分是`feature/aspnet_identity`的部分。

![](https://i.imgur.com/9Hkqj1n.png)

一樣運用本地追蹤分支的創建，user3開始修改，然後用`git push origin feature/aspnet_identity`的方式來上傳上去。

### user2合併
假設這次修改滿意\完整，我們就會讓這次修改分支合併回master上。

![](https://i.imgur.com/AOyvRzd.png)

我們這次對"hotfix/bugs_in_membership"修正完成了，我們用merge合併分支，並且push上去(因為已經建立好連結了，所以用`git push`可以直接做到上傳)。

### user3合併
在開發分支上的小分支，我們也完成新增修改的部分。所以我們想merge回到develop上，一樣用上述方法完成。

![](https://i.imgur.com/4YxuzfO.png)

如上圖，因為develop分支沒有在user3內，所以要建立一個本地追蹤分支。

### 處理結果
這些方支狀況用了一下子後，發現到，只要善用分支系統，不會像前一天學的時候，不斷遇到衝突發生，因為各個人都在不同分支上做自己的修正。而不會每次上傳檔案就直接發生衝突，然後想辦法解決，然後再發生衝突。

![](https://i.imgur.com/0vXNSnO.png)

這是上述動作最終狀態，可以看到目前還有分支進行中。

## 遠端儲存庫的狀況
而我們動作會對遠端有什麼影響呢?

### 新增標籤分支
我們在一開始新增一些標籤跟分支上去，我們可以在遠端看到。

![](https://i.imgur.com/vusX24v.png)

用github網頁查看，就可以看到這些分支標籤選擇。

### 修改分支版本
而我們修改了分支後，也會顯現在遠端上。像是下圖。

![](https://i.imgur.com/pKuUt5w.png)

今天我們做出了4個分支，跟創建了兩次的commit。

而我們創建的一些分支，因為沒有合併回主分支(master)上，所以出現了中間黃色的訊息。

在下方儲存庫狀況，會因為我們選取的branch版本而有不同，像是我們是在develop下，所以會有b.txt的檔案，並且可以看到a.txt後面有它最終修改版本的commit message，所以我們可以得知a.txt是還沒有經過fixbug的版本。

## 感想
善用分支版本，可以減少衝突發生 ~~(難聽點就是囤積起來之後解決)~~ ，並且有條裡有順序的修正bug和開發版本。
