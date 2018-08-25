# Day3
來製造版本分歧吧
## 分支影響
~~天下之事，分久必合，合久必分~~，只要不是全程都一人作業又想法都是沒有改變過的狀況，就會需要有不同版本並存的時候。難道每次版本更新前，都需要把整個專案複製一份起來才開始改動嗎?如果不備份，當修改程式方向錯誤要回頭時怎麼處理?這時候現在的我就覺得git中branch的方便處。或是文中提到的，難道一個人更新一個區塊，後來又被另一個人要更新別的區塊時覆蓋過去，才算是沒有用會衝突的分支嗎?這些簡單的例子，都是提到分支好的地方。當然，這大概也建立在好好管理的情況下吧。
## branch
因為我也不是很熟悉，總之先照著內容的例子來製造簡單的branch吧
### 來新增索引檔吧
```
echo. > a.txt
git add .
git commit -m "first commit"
echo 1 > a.txt
git add .
git commit -m "a.txt: set 1 as content"
```
這兩行，因為a.txt的新增和更動，製造出兩個小版本出來，而這些更動資訊都可以從`git log`中看到。這時候branch只有master一個，所以`git branch -d master`這種刪除master的方式還不能用。
### 製造分支
```
git branch
git branch branch1
```
第一行，就是簡單的查看當前分支，這時只會看到一個，之後`git branch branchName`就可以製造出新的分支出來，當然你不會立刻跳去該分支，還是在原本的分支上。而這分支索代表的索引檔，即是當前狀況的索引檔。我們可以發現，目前其實索引檔狀況還是一直線，只是代表目前branch有兩個在目前狀況的索引檔上

### master繼續前進，branch1繼續停留
```
echo master > b.txt
git add .
git commit -m "Create b.txt with content 'master' in the master branch"
```
這三行，就是製造新索引檔用的簡單指令，就是對目前狀況下新增b.txt並在裡面寫入"master"來表示我們目前是master的branch，而此時，可以知道branch1在剛才狀況下就被分支出去了，所以之後動作因為不是在branch1裡執行，並不會改變到branch1的內容。
### 新的分支
我們用`git checkout -b branch2`來新增branch2並跳去branch2裡。
```
echo branch2 > b.txt
git add .
git commit -m "Modify b.txt with content 'branch2' in the branch2 branch"
```
這邊我們修改了b.txt的內容，並製造新的索引檔，表示我們目前在branch2做動作。而這時候我們可以利用`git log`來查看狀況
![](https://i.imgur.com/TcADjUM.png)
圖片的文字有些不同就先不管，HEAD就是我們現在正在的索引檔位置，而綠色那些字，就是該branch最後的地方，如果那些branch之後有動作且新增索引檔，就會離開這段branch的log內容。
### 切換分支
剛我們創建branch2時就有看到`git checkout branchName`其實就是切換分支的方式，`-b`只是為了新增分支。
### 刪除分支
刪除分支重點在於，不能在自己裡面刪除自己，就好比自己在努力也無法把自己提起來一樣，都必須靠別人，所以我們刪除branch1時，就要在master或branch2裡面才能刪除。而刪除方式就是`git branch -d branchName`。
### 查看當前分支
用`git branch`即可知道所有分支並知道深綠色就是當前分支，也可以用`git status`來查看狀況，得知現在分支位置。
![](https://i.imgur.com/ZDaHPhN.png)
### 創件曾經存在的分支
因為我們練習中刪除了branch1，現在我想新增branch1回來怎麼辦?
```
git log
git checkout commitID
git branch newbranch1
```
方法關鍵就是索引檔，我們刪除的branch1，它的索引檔是第二次創建的索引檔，那時候修改了a.txt，用`git log`查看當時的commit id用`git checkout commitID`即使那邊沒有branch，也能切換到當前索引檔狀態，而這時後只要`git branch newbranch1`就能在此創建一個newbranch1而跟當時的branch1一樣啦。
```
git checkout newbranch1
echo newbranch1 > b.txt
git add .
git commit -m "Add b.txt in newbranch1"
```
這次我們也給newbranch1一個b.txt來說它是newbranch1吧!
### 樹狀圖
他使用SourceTree的工具來幫助他查看狀況。
在查看之前，因為我之前為了確認狀況所以多了些的指令，如下。
```
git checkout master
echo good > c.txt
git add .
git commit -m "add c.txt in master branch"
```
打算載SourceTree，卻需要登入，然後卡住了。只好用文章中的圖代替一下。而這圖就沒有對master做任何後續處理。

![](https://i.imgur.com/8Hdio9g.png)

由畫面可以看到，每個點就是每個索引檔，而每行所指的branch名稱分別對應到左方的索引檔點，而索引檔更新時間先後分別顯示在點的高低，最高的點最新，而最低的點最舊。
## 今日結語
經過一連串操作，我對於branch的新增、切換、刪除有初步的認知。未來要學會怎麼在好的時間新增、合併等分是操控又是另一堂課吧。
