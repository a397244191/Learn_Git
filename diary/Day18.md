# Day18
遠端儲存庫練習

## 建立一個repository
建立化面如下，最開始我們能命名並且是否做初始化。

![](https://i.imgur.com/1OAXRfj.png)

若只有名稱，就會獲得一個完全空的repository，github會有一些方式讓你完成建立，如下圖。

![](https://i.imgur.com/S26k1oh.png)

若選取一些初始化方式，像是下圖所做，就會有一個簡單的初始化狀態。
![](https://i.imgur.com/aqMHuXp.png)
下圖為初始化狀態。
![](https://i.imgur.com/BnH9jJp.png)

## clone後建立
我們知道我們可以用`git clone`來存取遠端儲存庫。對這兩個儲存庫的動作如下，雖然未做初始化的儲存庫有些警告，但是還是給你載了下來，而裡面只有`.git`檔案，而經過初始化的就會有一些一開始幫你初始化的檔案。
![](https://i.imgur.com/DSqOs6q.png)

### empty type
現在我們在emptybox的資料夾建立版本跟上傳到遠端儲存庫。

![](https://i.imgur.com/1AUNW3A.png)

因為內文因為遠端還沒有基本的master分支，所以要用`git push -u origin master`，我就突然好奇`git push`會發生什麼事，令我驚訝的，其實還是成功了，因為如上圖所見，它幫我建立了一個master的分支，這是我未能料到的。

### init type
這次來對初始化後的clone來做commit吧。因為已經建立好master分支，所以不需要用`-u`來操作，所以這次我乖乖的用`git push origin master`。

![](https://i.imgur.com/QEZlyYT.png)

動作大致一樣，只是少了一些遠端建立分支的工作，而經過第一次建立後，需要push時只要用`git push`就可以了。這個動作我在學習中也常常用到。

## 第二次push 跟push.default
總之來試試看push第二次吧，而我也順便檢查他說的設定。

![](https://i.imgur.com/cuAttUY.png)

可以看到它雖然是unset狀態(沒有顯示)，但似乎是預設為simple，所以git push時沒有跳出任何訊息。

## 本地資料直接建立遠端
這部份我們再次創建兩個repository，一樣一個是空的一個是初始化的。

### empty
我們想將local的東西連接上空的儲存庫。

![](https://i.imgur.com/DWATbmp.png)

如圖，這是在空的儲存庫，它建議的做法。只要經過remote連接上，就能將local的狀態上傳過來。

![](https://i.imgur.com/SKAfYLI.png)

照做後，就能成功上傳，而遠端也變成下圖。

![](https://i.imgur.com/IjZhiKw.png)

### init
這次來對初始化後的儲存庫做動作吧。

![](https://i.imgur.com/EmJhrgV.png)

這次我們做了跟之前一樣的動作，卻跳出一些error。其實學了十幾天了，也知道這狀況，就是兩邊狀態不對等而已。

#### 解決
方法很簡單，就是把遠端狀態pull回來，然後跟現在狀態merger即可。

![](https://i.imgur.com/hshiToZ.png)

這時候，有趣的地方來了，因為我的git版本是新的，所以上述動作無法操作，因為在`git pull`時，就因為沒有相同的歷史版本而遭到拒絕。所以實際方法是用`git pull origin master --allow-unrelated-histories`來做pull，而這裡也會幫你完成merge所以不用再自己弄一次。

![](https://i.imgur.com/yMTEJNn.png)

用`git log`可以看到origin/master已經在我們歷史紀錄內，也完成了merge動作，所以可以直接`git push origin master`來完成上傳到遠端儲存庫。

![](https://i.imgur.com/asX65mo.png)

## 感想
這裡看到我第一天開始學git時的狀況，覺得好懷念呢。也因為學了十來天，所以也知道狀況原因跟解決方式了。