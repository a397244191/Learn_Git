# Day5

獨一無二的名稱 

## commit id

每次`git log`後，就會出現一堆字，而其中最顯眼的就是那些黃色的亂序字串了，不過每個看起來混亂的字串，其實是經過一種hash的方式加密而成的。而這些字串就是我們的commit id 啦!

![](https://i.imgur.com/1qELmWx.png)

## 查詢內容

我們最常用的就是`git log`來查看一些簡單資訊，像是commit id 、作者名稱、日期、及他的簡介。而我們看到commit id後，便可以利用這些id來查詢更多內容，利用`git cat-file -p [commitID]`，來查看它所在的樹ID和它前一個parent的ID等。

![](https://i.imgur.com/9VNYbgb.png)


## id縮寫

人是一種常常需要偷懶的生物，何況commit id沒有簡單規律又長的跟什麼一樣，總不能一一背下來吧?所以這長長一段又叫做「絕對名稱」，而絕對名稱呢，可以用4~40個字元都可以表示相同的「絕對名稱」。

### --pretty=oneline
有時候用`git log`時，我們其實沒有想要很多資訊，只是想查詢id，這時候打成`git log --pretty=oneline`就能把整段只留下id和裡面簡介而已，對當你commit很多次後，在一大串東西裡面找更簡單可以找到你要的id。

![](https://i.imgur.com/5QyeOPW.png)

### --abbrev-commit

剛剛也提到絕對名稱4~40個都可以拿來表示，所以有了這個參數，加上這參數後`git log`的 commit就會剩下前7位來表示，更方便查看東西，而跟前一個`--pretty=oneline`同時使用，你就能看到清楚簡單的列表了。

![](https://i.imgur.com/V5kJUgg.png)

## 今日結語

認識了絕對名稱後，我終於不用再像之前一樣，把一整段commit id打上去，有時後一大段看的也挺眼花的。
