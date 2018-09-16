# Day23
即使沒用過還是來認識一下。內容因為沒有手邊範例，所以就是紀錄一下看到的內容。

## SVN
我也沒認識很多就不多提了，Subversion(SVN)是一種版本管控的系統，而今天看的是把SVN改成Git管理。

## 使用者清單
在SVN中，使用者只有名稱，而git卻需要名稱跟email，所以要先做這修改。

在此文內假設一些名稱
- SVN 專案網址：`https://svnrepo:23443/svn/DoggyLibrarySolution`
- SVN 工作目錄：`D:\Projects\DoggyLibrarySolution`
- GIT 安裝路徑：`C:\Program Files (x86)\Git`

在SVN工作目錄下執行指令
```
D:\Projects\DoggyLibrarySolution$SET PATH=%PATH%;C:\Program Files (x86)\Git\bin\
svn log --quiet --xml | sed -n -e "s/<\/\?author>//g" -e "/[<>]/!p" | sort | sed 
"$!N; /^\(.*\)\n\1$/!P; D" > SVNUsers.txt
```

會得到一份開發人員名單的檔案(SVNUsers.txt)，當然上面只有名稱。接下來是要去修改這些內容以便配合git

`svnuser = GitUsername <GitEmail>`

將所有內容都改成上述模式，前期準備就完成了。

## 專案取出改成git目錄
先假設git工作目錄在`G:\DoggyLibrarySolution`，我們先將剛剛修改過的SVNUsers.txt複製到`G:\`下，然後執行。

`git svn clone https://svnrepo:23443/svn/DoggyLibrarySolution --no-metadata -A SVNUsers.txt --stdlayout`

而如果權限只有`/trunk`，此時不能使用`--stdlayout`。當指令執行後，可能需要做登入動作。而轉換完後就會得到一個git儲存庫。

## 忽略清單
就如同git有`.gitignore`一樣，svn也有，可是這被分散到各個目錄屬性中。

`git svn show-ignore`

上述指令可以將你把那些忽略清單整合，但也可能出現問題。

`G:\DoggyLibrarySolution>git svn show-ignore
config --get svn-remote.svn.fetch :refs/remotes/git-svn$: command returned error: 1`

若跳出上述的狀況，可以加上`-i trunk`的參數。而當你確認好忽略清單整合後，可以用下面的指令建立起`.gitignore`。

```
git svn show-ignore -i trunk > .gitignore
git add .gitignore
git commit -m "Create .gitignore from SVN"
```

## push遠端
當你做好這些東西後，總不會是自己使用而已吧?所以要放到遠端上。

文中因為github是預設公開，所以改用了 [Bitbucket](https://bitbucket.org/) 來建立私有的專案。

建立後就跟之前提的一樣連接remote然後push上去就完成了。

## 題外話
文中最後提到，這工作目錄還是可以跟SVN做溝通連接，至於這些操作就`git help svn`便可以知道完整方式。

## 感想
雖然沒用過svn，但也因為這部分去看了一些資料，認識了一下它。算是因此增廣見聞吧?
