# Day2
簡單操作開始 
## 基本用法
昨天一個想先弄好就拋下一些指令介紹，今天要來一個一個嘗試看看
### git add
上次也用過這個，這次看過一些git內部資料狀況的介紹後，有些更明白他放的地方了。簡單說就是將檔案寫入索引檔開始追蹤紀錄下來用的。
用法就是大致如下:
- `git add .`
  - 將工作目錄下全部檔案寫入「索引檔」
- `git add [filename]`
  - 對檔名為filename的檔案寫入「索引檔」
- `git add [xxx*]`
  - 對檔名為xxx開頭的檔案寫入「索引檔」，* 代表不指定字
- `git add -u`
  - 對「更新」跟「刪除」的檔案寫入「索引檔」
簡單認識了一些不同用法後，也對不同用法有不同認知。
### git rm
rm 也就是remove的縮寫，就是刪除的意思啦，將工作目錄下的某些東西刪除就會用到它。而特別的是，用`git rm [filename]`會將檔案從索引檔中刪除，也會把檔案本身刪除，如果要避免刪掉原檔，就用`git rm --cached [filename]`來只將檔案從索引檔刪除，它的實體檔案還會留存。
### git mv
就是改名啦，可以將舊檔案改成新檔案名稱。`git mv [oldname] [newname]`
### git commit
對目前最新檔跟索引檔比較，將差異題出commit物件，`git commit -m "xxxx"` xxx為簡單版本文字說明，`git commit`會呼叫一個編輯檔，編輯完儲存並關閉編輯畫面，便會製造commit物件。
### git ls-files
就是索引檔目前所有檔案的list。
### git reset
就是重置索引檔內容，將索引檔回復狀態，但是被刪除的實體檔案不會回來。若要將工作目錄也回復到目前最新版本狀態就用`git reset --hard`
### git checkout
`git checkout master [filename]`會將master最新的檔案還原，這樣可避免`git reset`一次回復太多狀態。
## push 失敗?
本來打算今天這樣就收工，把Day2 push上去時出現了一些問題，google答案後，用newbranch的方式，merge完在push就成功了。
## 今日結語
試用了一些指令，了解了一些git構造，算是對git有一定認識了吧。
