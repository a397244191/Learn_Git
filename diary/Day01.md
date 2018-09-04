# Day1
總之有開始都是好事
## 安裝
照著上面裝了git for windows和github for windows，可是果然看commend line會比較有感，所以打開cmd開始看看
## 創建repository
先在git內創建repository。然後到要連結git資料夾`git init`做初始化
## 如何開始檔案管理，就是有檔案
他用`yo webapp`來下載一份檔案，然後開始操作，不過我嘗試用之前寫好的code來做看看
### git add .
檔案一進到主機端的資料夾裡，可以用`git status`來看到，裡面放的檔案都是紅色顯示。
![](https://i.imgur.com/inWm2cA.png)

使用`git add .`就是將本資料夾內的所有檔案更新。
![](https://i.imgur.com/EBJZD55.png)
 
### 第一次 push
文章內後面都是在做一些local的檔案管理，像是commit、rm...等，不過我想先嘗試上傳的感覺，就照著開啟repository的介紹三步驟跟著打
1. 做好commit
2. 連接到我要傳的git位置
3. push上去

![](https://i.imgur.com/e39GDFr.png)

做完這裡，我的readme上去啦!
### 第二次 push
欸？push不是一樣嗎？怎麼沒反應。
這次我把code部分放進去了，開始add，然後做到push出現錯誤？總之照著嘗試`git pull`好像做到什麼合併了。再用`git push`後就成功了？

## 今日結語
看了好多東西介紹，有點暈頭，今天就先到這裡好了。
