# Day8
windows相關設定

## 設定
這次目的就是去認識windows下的查看設定不同、修改和一些常見設定。而這些都跟`git config`有關

### 查看
`git config --list`就能列出當前的設定狀況。而接下來要介紹三種常見分類參數。
- --system
  - 系統層
    - 但若是使用UAC模式的command line是一般模式下時，儲存到的資料夾會跟系統管理員開啟的不同。
- --global
  - 使用者層
    - 儲存在該使用者的資料夾下。
- --local
  - 儲存區層
    - 就是git init後，會有一個設定檔`.gitconfig`裡的設定。


### 特定值
- 查看
  - `git config [Name]`
- 修改
  - `git config [Name] [value]`
- 刪除
  - `git config --unset --[type] [Name]`
    - `--type`就是指前面說的三種層級，畢竟三種各自會有各自的儲存位置，所以刪除時要特別指定，至於修改上，會自動對應到相對的位置，如要特地指定也是能加上。

### 套用層級
優先度跟權限相反，有點說是個人化的做法。例如前面提到的三種層級會是：
1. system
2. global
3. local

local最後套用，因為他優先度最高，所以假設有一格值被system設定過，local也設定過，最後設定值會是local。

### 設定檔
可以用`git config --[type] --edit`來直接開啟設定檔的檔案做修改，就不用去資料夾一個一個開了。

## 常見設定
有些會被常常設定的東西。

### 別名
`git config alias.[Alias] [command]` 就能讓一些常用的[command]有個[Alias]的別稱。這樣之後只要用短短的[Alias]來打，節省時間和方便工作。

### CRLF
`core.autocrlf true`會將檔案過濾`\r`來方便整合跨平臺檔案。

### 訊息顏色
`color.ui auto`預設是已經開啟，如不小心關閉可以開啟。

### commit 訊息範本
有需要可以預先設定好樣式，方便之後commit可以不用都把模版從頭一遍。
不過這建議用在`--local`上，畢竟每個專案常常會有需要不同的樣式。

## 今日結語
今天主要就是設定自己的git工作環境的部分。很有幫助，但暫時不會需要。
