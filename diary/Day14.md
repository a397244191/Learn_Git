# Day13
回復狀態

## 修改commit
當我們發現，三天前改版內容大錯特錯，甚至影響之後所有版本時怎麼辦?我要回復到可能30個版本前，然後一一修改新增回到現在版本嗎?

### git revert
`git revert [commitID]`就能將該次版本修改的內容反轉。什麼是反轉呢?這時候就用`git show [commitID]`來看就知道了。

![](https://i.imgur.com/xPE4ab2.png)

可以看到`git show 888f`得知我們在那版本修改了a.txt哪個部分。而後我們用`git revert 888f`後跳出了commit給我們修改。便產生了一個新的版本，內容是將`888f`的內容修改回去。

### revert須知
其實revert就是查看你版本做的修正，做了反向操作，然後merge回現在的版本而已。而因為是merge，所以一定會有發生衝突的時候。

### 衝突的revert
現在我們稍微修改了a.txt的內容並新增一個版本。

![](https://i.imgur.com/tHjVW7l.png)

並也執行了`git revert 888f`，欸?怎麼不一樣的東西跳出來了，用`git status`一看，原來是merge發生衝突了。

按照之前的方式，重新修改commit一次，就完成衝突解決了。

### 不commit行不行?
有時候，回復後還不夠，因為有些只是刪除錯誤，可是後來還要新增東西之類的狀況，就會需要暫時不commit的動作。

![](https://i.imgur.com/y6jvB8Z.png)

我們稍微又找了一個版本4048，他是新增stage1.txt的檔案。我們使用`git revert -n [commitID]`就能回復版本，但停在`git add .`的狀態。用`git status`來查看，就能看到revert已經完成了。

這時候我們有兩種辦法可以做。

- `git --continue`
  - 完成修改後輸入，就會跳出版本資訊修改，結束後新增版本。
- `git --abort`
  - 發現版本回復錯了，或是修改的不甚理想，想要放棄這次版本修改就能用。

所以revert後，commit不是用`git commit`來做，而回復狀態，也不是用`git reset --hard`回復。

## 感想
這次學會了一個新招，雖然不知道用法該用的狀況會是什麼。不過用了這種方式，修改不再只是修改，還能跟舊版本有所關連，是個比較有邏輯的修改方式。