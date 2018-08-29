# Day6
自行取名

## 參照名稱
看到commit id不管再怎麼短，都不是自己給的，總是會覺得難以記憶，可是每次想要去紀錄一個commit就要給它開branch嗎?今天認識的參照名稱(ref)就很好用。

### 常見的參照名稱
其實我們開的branch取的名字就是參照名稱，只是它還有包含很多功用，今天就來單純介紹名稱的用途。打開位在`.git/refs/heads`裡面的一個參照名稱可以看到下圖。而參照名稱除了用在commit上外，tree物件、blob物件等有絕對名稱的物件上。

![](https://i.imgur.com/0I6Bpbc.png)

裡面有一個commit id，這就是讓我們名稱可以指引到對應的commit id的方法。

### 參照名稱使用
我們只要打`git cat-file -p secondbranch`就可以查詢`c1dd`的資訊，但這時有個疑問了，明明它的位置是`.git/refs/heads/secondbranch`呀?為什麼可以不用寫路徑?

其實原因很簡單，就是git會自動去搜尋`.git`下的所有名稱。

### 符號參照名稱(symref)
就是那些git先幫你設置好的一些名稱，幫助你發生狀況使用。以下舉些例子

- HEAD
  - 其實這在branch時就看到不少次，就是指當前最新的版本。
- ORIG_HEAD
  - 就是當前最新版本前一個版本。
  - 不過在沒有push前都不會出現，我在練習用的資料夾看了半天沒找到，去別的就看到了。
- FETCH_HEAD
  - 遠端儲存庫，可能會用 `git fetch` 取回所有遠端儲存庫的物件。這個 FETCH_HEAD 符號參考則會記錄遠端儲存庫中每個分支的 HEAD (最新版) 的「絕對名稱」。
  - 不過在沒有push前都不會出現，狀況同上。
- MERGE_HEAD
  - 當你執行合併工作時，「合併來源｣的 commit 物件絕對名稱會被記錄在 MERGE_HEAD 這個符號參照中。
  - 不過還沒merge過，不知道狀況。

### 創建參照名稱
`git update-ref Name commitID`就能創建一個參照名稱給特定commitID，不過這裡要注意的是在刪除上。我用`git update-ref -d Name`時遇到的狀況。

![](https://i.imgur.com/78ifEO1.png)

查的資料是說，因為指令較為底層所以更嚴謹的只去找refs裡的id不會去猜測你的位置，所以在創建參照名稱時，最好都用`refs/Name`來使用，而實際測試也發現，加上`refs`後就不會有問題。

### 查看
`git show-ref`就能看到目前所有參照名稱

![](https://i.imgur.com/WbdtGNO.png)

### symref創建
`git symbolic-ref Name branch`這樣做法，Name裡面就會有包含branch的資訊並追蹤它，就能做到跟內有的HEAD有相同效果。這實在很神奇。

## 今日結語
看了一堆給名稱跟名稱的用法後，除了發現它的用處外，更是發現不少它神奇的方法。感覺這些東西越來越有趣了。

