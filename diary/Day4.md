# Day4
我們哪裡不一樣?
## git diff

`git diff`這指令可以簡單的知道兩個版本不同之處。

### 如何看懂差異

![](https://i.imgur.com/oRIqASZ.png)

以這為例，我對昨天的master跟branch2兩個branch來做diff。在顯示上會將前者用a代替，後者用b。然後一一筆對裡面有不同的檔案。而沒有不同的檔案則不顯示，如範例裡面應該要有a.txt卻沒有，因為兩者一樣。而內容中，有紅色'-'的是a版內有的b版沒有的，而綠色'+'則是b版內才新增的，所以如果把同一行改成別的句子就會同b.txt裡面那樣各出現一行。而沒有出現的檔案，則會在b版中以/dev/null顯示表示一個空的檔案。

### 常見的不同方法

- `git diff`
  - 這行看似沒有加任何比較的東西，其實就是比較目前目錄上(workspace)的狀況跟當前索引狀況。
    - 在更新檔案後常常會`git add`幾次，而在`git add .`前，用`git diff`可以查看更改了什麼?
- `git diff commit`
  - 在`git diff`後加上一個commitID，這是讓這個commit來跟workspace做比較。
    - 常用`git diff HEAD`即可查看跟最新commit的版本差異。
- `git diff --cached commit`
  - 不同於前兩者，被比較的不在是workspace，這裡是目前的索引檔，而它的比較對像則是目前最新版本的索引檔。
    - 與前者不同是，沒有被`git add .`過的東西不會被查看到。
    - 也是最常用`git diff --cached HEAD`來查看`add`的東西和最新commit的版本差異。
- `git diff commit1 commit2`
  - 很直接的，拿了兩個版本做比較。
    - 常見的方式有`git diff HEAD^ HEAD`或是`git diff HEAD~2 HEAD`分別是讓所有commit的版本中，最新前一版跟最新版，和最新前兩版跟最新版的比較

### HEAD

HEAD即為目前最新版本啦，而`HEAD^`的'^'則是指前一個版本，而`HEAD~N`的'~N'則是前N個版本的意思，N是任一個數字。

而windows的cmd裡面有趣的是，'^'被拿來表示還沒打完，所以要用'^'來查看時要寫成`HEAD^^`來代表這裡的`HEAD^`啦。

## 圖解說明

因為上述打完，我自己也有點搞不懂它們那些的關係，所以用圖來嘗試再看一次

![](https://i.imgur.com/0w5bKDs.png)

其中A就是我們`git log`可以看到的狀態。而我們先假設A是最後一次commit。則A也就是HEAD。

以下我們在來看看上述4個用法前三個。

- `git diff`
  - 比較對象是B和workspace
- `git diff HEAD`
  - 比較對象是A和workspace
- `git diff --cached HEAD`
  - 比較對象是A和B

簡單打成這樣，我似乎也明白一些。

## 今日結語

簡單的用了diff並了解diff用法上分別比對了什麼後，希望在之後我能善用diff來檢查我的狀況。