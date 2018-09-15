# Day22
沒有什麼操作

## 個人專案
一個專案，你可以利用github裡的Collaborators來設定一些人選。被你設定的這些人呢，就可以對該專案做push和pull的操作。

![](https://i.imgur.com/fVyDScU.png)

如圖，在內打入帳號後加入他，就賦予他權限來操作你的專案。

## 組織帳號
這部分因為沒有，所以我就讀過去而已。

在一個組織帳號內，你可以設定團隊權限，可以分成"僅供讀取"、"可以修改"、"修改外加專案管理"三種。至於狀況真遇到再來看看會更清楚吧。

https://github.com/doggy8088/Learn-Git-in-30-days/blob/master/zh-tw/28.md

## fork
fork就是叉子，每個專案就像在對方盤中的美食，你可以利用叉子來叉取對方的食物 ~~(但實際上又不會減少，這很奇怪)~~ 。雖然對方專案你沒有權限操作，但用fork就能將對方專案複製一份過來你的儲存庫中，有點像是clone但你是在遠端儲存庫做。而你的新專案會有被註"fork form"的訊息。而fork完後，這份東西就會在你權限可及的帳戶下，所以你便可以對它做任何操作。

## pull request
而我們fork後，有時候會覺得這個修改太棒了 ~~(自我感覺良好?)~~ ，會想將這份fork出來的部分丟給原本那位擁有者看甚至合併回去。但礙於沒有權限，最多我們只能去請求(request)對方。我們拿上次用的emptybox專案試試，點選pull request，選取檔案(當然這裡用了上次修改的develop分支)。

![](https://i.imgur.com/RI38E5w.png)

可以看到，在沒有衝突的情況下，下方會顯示更新的部分，上方會出現"Able to merge"的字樣，這時候只要create pull request就可以了。

![](https://i.imgur.com/7VmAz5j.png)

可以看到，除了commit message外，還可以告知一些訊息給擁有者。在次按下"create pull request"就完成操作了。

![](https://i.imgur.com/C9vsob5.png)

而另一方的擁有者可以看到上圖，如果覺得可以merge就會按下"merge pull request"來merge這次的部分。

## 感想
雖然fork跟pull request感覺經過很多道手續但也是正常的，畢竟不能每個你要看的專案都去要求使用者給你權限，甚至讓你直接修改吧。今天沒太多操作部分，畢竟有些是需要切換帳號之類的才做得到。~~(但沒事為了這個去辦帳號也挺累的)~~