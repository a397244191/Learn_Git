# Day9
重要的地方上標籤，從以前到現在都是。

## tag
標籤分成兩種
1. 輕量標籤 (lightweight tag)
2. 標示標籤 (annotated tag)

而我們可以利用`git tag`來查看當前所有標籤。

### 輕量標籤
輕量標籤就跟參照名稱一樣，指向一個commit id。用`git tag [tagName] [commitID]`來對特定commit做tag，若是沒有commit id 就是指HEAD(當前版本)。而刪除tag的方式就是用`git tag [tagName] -d`來刪除。

![](https://i.imgur.com/iqpe7OB.png)

### 標示標籤
這有所不同的地方在於，輕量標籤只是個名稱，他的type還是他所指向的commit，但標示標籤就不一樣，他是一個物件。

![](https://i.imgur.com/7PscVLv.png)

由圖可知，經由`git cat-file -t`可以知道他是一個tag物件，而用`git cat-file -p`後，裡面第一行是object來看，表示他可以tag任何物件。

而新增一個標示標籤的方式是`git tag [tagName] -a -m "some comment"`，其中`-a`是當前版本，可以用`[commitID]`代替成其他commit，而`-m ""`是替該tag標示一些資訊。

## 今日結語
標上標籤後，可以對特定版本做紀錄，方便之後去查看過去改版狀況。
