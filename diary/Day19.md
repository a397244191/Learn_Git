# Day19
遠端儲存庫使用。

## 基本動作
牽扯到遠端儲存庫後，有一些必須知道的指令。

- `git clone`
  - 複製遠端儲存庫，並在本地建立工作目錄。
- `git pull`
  - 將遠端儲存庫最新版下載過來，並merge到本地master。
  - 等同於使用`git fetch`和`git merge origin/master`
- `git push`
  - 將本地目前相關物件傳上遠端儲存庫。
- `git fetch`
  - 下載遠端儲存庫最新版。
  - 不會做merge動作。
- `git ls-remote`
  - 顯示特定儲存庫的參照名稱。
  - 遠端分支與遠端標籤

## 分支
在local端有些分支的使用，但加入遠端儲存庫後，又有一些遠端分支需要知道。

分支在文中分成四類，遠端分支、遠端追蹤分支、本地分支跟本地追蹤分支。雖然看起來是遠端有兩種分支本地也是，但其實詳細看完其他地方資訊後發現，其實只有遠端分支存取在遠端儲存庫。其他分支都是在本地儲存庫中。以下來一一細說。

- 遠端分支
  - 就是在遠端儲存庫的分支。只要能訪問那個遠端儲存庫就能看到。
- 遠端追蹤分支
  - 經由`git clone`後下載過來的遠端分支，一般是不會看見及使用的，但如果用`git branch -a`或`git branch -r`就可以看見。
- 本地追蹤分支
  - 對於遠端分支來說，通常不建議去直接修改它們，而是在本地建立分支追蹤它們再來做更新。
  - 可以利用`git branch --track [remote-tracking branch]`或是`git branch -t [local-tracking branch] [remote-tracking branch]`來建立本地追蹤分支，前者會直接用遠端追蹤分支名稱當做本地追蹤分支，而後者會給定一個本地追蹤分支名稱。
- 本地分支
  - 就是純粹建立在本地的分支，跟遠端儲存庫沒有關聯性。通常是用做開發用途，而也被稱為Topic Branch或Development Branch。

![](https://i.imgur.com/3vtG7oi.png)

上圖是一些分支操作。我們可以看到我們從jquery clone下來的資料夾中，只有看到master分支。這是本地類的分支，而用`git branch -a`可以顯示所有分支，包含紅色的遠端追蹤分支跟綠色的本地類分支。而master其實就是一種本地追蹤分支，它是追蹤`origin/master`這個遠端追蹤分支。

而我們用`git branch newbranch`建造的是本地分支，它跟遠端追蹤分支沒有關係，所以不會被git跟遠端儲存庫的動做存取到。而`git branch -t newbranch2 origin/1.12-stable`就是產生一個newbranch2的本地追蹤分支，而它是追蹤`origin/1.12-stable`這個遠端追蹤分支。而因為它跟遠端追蹤分支建立關聯，所以當`git push`跟`git pull`時就會跟newbranch2有關係，push會將newbreanch2藉由遠端追蹤分支跟遠端分支合併。而pull時會將遠端分支藉由遠端追蹤分支做合併。

說起來有點饒舌，不過雖然可以藉由本地追蹤分支跟遠端追蹤分支來修改遠端分支，可是在大多數情況下，除了master分支外的這兩個追蹤分支還是當做唯讀狀態 ~~(看看就好)~~ 不要去做任何操作。

## 連接遠端儲存庫
我們在上次操作中有使用過這類型的指令，像是`git remote add origin https://github.com/doggy8088/sandbox-empty2.git`。而這指令就是去連接遠端儲存庫用的，而origin是一般我們預設的遠端分支參照名稱，代表後面一串的URL。而要看當前有什麼遠端儲存庫了話，可以用`git remote -v`來查看。

![](https://i.imgur.com/XBPTJFy.png)

我們可以看到上次操作後的名稱，而前面origin就是後面URL的參照名稱，而最後fetch跟push就是指使用`git fetch`(`git pull`包含了`git fetch`的事情)和`git push`時會去參考的部分。

而我們可以用相同敘述`git remote add [refName] [remote-URL]`來新增，像是在這個emptybox2內去存取jquery的東西試試看吧。

![](https://i.imgur.com/tzujYJL.png)

從`git remote -v`來看，可以確定我們連線成功了 ~~(?)~~ 。

## 抓取遠端資料
接下來我們想用`git fetch`將jquery的東西載到本地上。

![](https://i.imgur.com/EKNQwgQ.png)

如上圖，因為有一堆tag所以省略中間一大半的訊息，大致上可以看到，下載遠端資料跟在本地設立了遠端追蹤分支跟標籤。而如上面所說，這些分支都是遠端追蹤分支，所以我們在看`git branch`的時候不會看見。

## 查看連接設定
我們可以利用`git config -l`或是去查看`.git/config`來得知當前remote狀況。

`git config -l`

![](https://i.imgur.com/1oUjYZb.png)

`.git\config`

![](https://i.imgur.com/Mg4I3cN.png)

這裡可以看到一些跟遠端的關係資訊，大約可以分成remote origin是哪個url而fetch連接是哪些連接，而本地的master是連接到哪個remote，而merge會merge去哪個branch內容。

### 參照名稱對應規格(refspac)
一個規格`+refs/heads/*:refs/remote/origin/*`可以切成四部分。

- \+
  - 代表傳輸資料時，不會特別使用安全性確認機制。
- `refs/heads/*`
  - 遠端儲存庫的遠端分支。而* 代表以下所有。
- \:
  - 區隔來源(左邊)跟目的(右邊)
- `refs/remote/origin/*`
  - 代表本地的本地追蹤分支，* 一樣代表以下全部。

這些設定會影響的操作關於`git fetch`跟`git push`。

### fetch
知道規格是長怎樣後，我們就可以開始做一些修正。像是把fetch改成`fetch = +refs/heads/master:refs/remote/origin/master`，在操作`git fetch`就只會做跟master有關的部分。

而若有特定分支需要被連接，也可以設定多個。像是文中範例。
```
[remote "origin"]
       url = https://github.com/doggy8088/sandbox-empty2.git
       fetch = +refs/heads/master:refs/remotes/origin/master
       fetch = +refs/heads/TestBranch:refs/remotes/origin/TestBranch
```

### push
上面已經提到如何新增修改，只要將fetch改成push就可以了，但是為何沒有push的設定呢?通常push都被預設成`push = +refs/heads/*:refs/heads/*`，如果有要修改再新增上去即可。

而無論fetch或是push，只要沒預先生明用哪個remote都會預設到origin這區域。

## 遠端跟本地關係
通常我們在push跟fetch上都只有在master操作，而如果今天要對一個branch跟遠端做連接呢?`git push`肯定不會直接理你。要用`git push [remoteName] [branchName]`才能push上去，而這動作會讓遠端儲存庫新增一個遠端分支來存取你的本地分支，而你會獲得一個新的遠端追蹤分支。但這時候還沒有做到完全設定，你必須用`git push --set-upstream`後，你的本地分支就會 ~~進化~~ 變成本地追蹤分支。並且連接內容會新增在`.git\config`中。這也表示你在這分支中做push會直接對應到遠端的這個分支上的意思。

而master的這些設定我們怎麼沒做呢?因為在一開始的`git clone`或是第一次的`git push`中就會設定好了。

## 感想
這部分提到很多git上的遠端儲存庫的內容跟需知，現在回想起來，之前利用一些clone去自行做編譯一些工具時都只會傻傻的跟著做，現在知道更多知識後會想到當初其實可以不用一直刪除重載刪除重載，用git的一些指令便能確保狀態還原了呢。