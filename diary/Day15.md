# Day15
撿櫻桃

## 使用情境
開了新分支，做了新更改，發現狀況很糟被改爛了，想刪除他卻發現裡面包含著一些好的更動。這時候就來撿櫻桃吧，把沒爛掉的櫻桃撿回來就可以了。

## 行前設定

![](https://i.imgur.com/XVoV88m.png)

經過一連串簡單的更動後，目前git狀態是長這樣子，我最初在master上新增a.txt，然後更新a.txt，開分支(branch1)然後在branch1上更新a.txt、新增b.txt、再更新a.txt。之後切回master更新了a.txt後是最新的狀態。

##  cherry-pick
`git cherry-pick`就是在後面接上需要保留更動的commit，跟上次提到的resert很像，只是resert是反向操作commit，這是正向。

![](https://i.imgur.com/tr4AMLB.png)

如圖，我們把`add b.txt`那則commit加回到master分支上。可以看到`git log`結果是加入了一個commit，而且有趣的是，該則commit上的內容，除了絕對名稱外，都跟之前分支上的內容一樣，包含Date跟Author，所以這裡出現了最新的commit時間卻比舊一則的commit晚的狀況。

## 其他參數
關於衝突的部分就不多提，畢竟狀況根解決方法都看過了，之後要說說他的不同參數下的結果。

大致上有分三種參數`-x`、`-e`、`-n`。

### -x
`-x`參數後，就會再commit裡新增一則關係。

![](https://i.imgur.com/IbX6iKU.png)

會讓人得知它從哪裡來，可是大多時候這是為分享的版本，當你分享版本後那個分支早就消失了阿?你給這個絕對名稱也沒有意義。所以大多時間都不會用到，除非是在修改已上傳到遠端儲存的版本才需要。

### -e
就是編輯commit的意思，他不會直接建造版本，而是讓你修改一下內容再commit

![](https://i.imgur.com/ZHUDRYI.png)

### -n
這就是說暫時不要新增版本，還需要一些更動，所以下參數後，會先暫時放進索引檔裡，等一切就緒後就commit它。這時候，commit的版本就會是你自己的版本，而不是從分支上拿來的版本資訊。

![](https://i.imgur.com/kmylNuU.png)

## 感想
看了這麼多修改commit關係的方式，我還是覺得好複雜不好找到使用時機。這也只能用經驗慢慢摸索吧。