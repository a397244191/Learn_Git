# Day13
忽略檔案

## .gitignore
這是一個清單檔案，會幫你過濾不需要追蹤的副檔名，之後當執行`git add`和`git status`都不會看到。

### github上設定
當你建立一個repository時，會有一個`ignore`的選項，你可以選擇接下來專案的主檔案，它會自動列出清單幫你過濾其他檔案。

![](https://i.imgur.com/wZp4egN.png)

### 內容
可以看看裡面的內容

```
# Build Folders (you can keep bin if you'd like, to store dlls and pdbs)
[Bb]in/
[Oo]bj/

# mstest test results
TestResults

## Ignore Visual Studio temporary files, build results, and
## files generated by popular Visual Studio add-ons.

# User-specific files
*.suo
*.user
*.sln.docstates

# Build results
[Dd]ebug/
[Rr]elease/
x64/
*_i.c
*_p.c
*.ilk
*.meta
*.obj
*.pch
*.pdb
*.pgc
*.pgd
*.rsp
*.sbr
*.tlb
*.tli
*.tlh
*.tmp
*.log
*.vspscc
*.vssscc
.builds

# Visual C++ cache files
ipch/
*.aps
*.ncb
*.opensdf
*.sdf

# Visual Studio profiler
*.psess
*.vsp
*.vspx

# Guidance Automation Toolkit
*.gpState

# ReSharper is a .NET coding add-in
_ReSharper*

# NCrunch
*.ncrunch*
.*crunch*.local.xml

# Installshield output folder 
[Ee]xpress

# DocProject is a documentation generator add-in
DocProject/buildhelp/
DocProject/Help/*.HxT
DocProject/Help/*.HxC
DocProject/Help/*.hhc
DocProject/Help/*.hhk
DocProject/Help/*.hhp
DocProject/Help/Html2
DocProject/Help/html

# Click-Once directory
publish

# Publish Web Output
*.Publish.xml

# NuGet Packages Directory
packages

# Windows Azure Build Output
csx
*.build.csdef

# Windows Store app package directory
AppPackages/

# Others
[Bb]in
[Oo]bj
sql
TestResults
[Tt]est[Rr]esult*
*.Cache
ClientBin
[Ss]tyle[Cc]op.*
~$*
*.dbmdl
Generated_Code #added for RIA/Silverlight projects

# Backup & report files from converting an old project file to a newer
# Visual Studio version. Backup files are not needed, because we have git ;-)
_UpgradeReport_Files/
Backup*/
UpgradeLog*.XML
```
而如果需要再新增一些檔案名稱，也可以自行修改。

### 參考其它
而github裡的預設檔案有分很多種，哪天到也可以稍微看看。

### 稍微測試
對現在正在練習的小專案放入`.gitignore`後，刪除一些被追蹤的檔案，看到以下效果。

![](https://i.imgur.com/jNk3QyF.png)

對於有`.user`的檔案將不再看到，這便是這檔案的效果。

## 感想
對於有時後，只是local自行產生對專案沒意義的檔案時，就會需要這些方式幫忙不讓專案追蹤它們。