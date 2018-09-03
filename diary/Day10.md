# Day10
歷史紀錄追蹤

## 紀錄內容

![](https://i.imgur.com/yOZNA9v.png)

上圖可見，右邊是在`.git\log\HEAD`的內容(截取後半)，左邊是用`git reflog`來查看，這兩個方式都可以查看你對HEAD做的操作紀錄方式，而指令跟檔案不同的地方，只是上下順序不同，指令最上層的部分是最新的。

### 復原版本
`git reset ref@{N} --hard`，就能回復狀態到HEAD@{N}的狀態，例如下圖。

![](https://i.imgur.com/MEyYvTB.png)

從最左邊絕對名稱就能得知，我們復原到上一個版本，而如果要回復原本回復前的狀況 ~~(好饒舌)~~ ，其實只要再用一次`git reset HEAD@{1} --hard`就能回復。

### 什麼動作會新增紀錄
基本上，只要有對版本有做出動作的都會有，像是切換branch、commit、merge、reset、stash...等，都會有新的紀錄被保留。

### 詳細資訊

![](https://i.imgur.com/ixUdBq8.png)

上圖可見，用`git log -g`就能看到詳細的紀錄資料。

### 刪除
`git reflog delete ref@{N}`就能將特定的紀錄刪除。而這些刪除，也只是在紀錄上刪除，而不會影響遠端儲存庫。

### 過期時間
利用上次學到的`git config`來做一些設定，可以讓管理自動捨棄掉時間過長的紀錄。預設上，git會幫你保留90天。而如果不希望被自動過期刪除就用。
```
git config --global gc.reflogExpire "never"
git config --global gc.reflogExpireUnreachable "never"
```

而後面加上期限，就能設定時間，例如下面範例的7天。
```
git config --global gc.reflogExpire "7 days"
git config --global gc.reflogExpireUnreachable "7 days"
```

至於後面字串要如何寫給git處理，可以參考C語言版本：http://git.kernel.org/cgit/git/git.git/tree/date.c 

### 清除歷史
用`git reflog expire --expire=now --all`可以清除所有歷史紀錄。而也可以用`git gc`來清除找不到或是沒被追蹤的紀錄。


## 今日結語
某意義上，今天認識了git的自動日紀功能 ~~(?)~~ ，對它的操作也有一定認識。
