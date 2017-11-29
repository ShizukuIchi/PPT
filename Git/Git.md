## Git 版本控制
>不會 *git* ，不會懂得 *git* 的美好。  
*Git* 簡單來說就是 *Coding* 界的時光機、平行世界、SL大法。

開始前需要存放 Code 的雲端空間，如 Github、Gitlab、Bitbucket等，建立帳號、數據庫等等動作不在此說明。

要注意的是，數據庫中的狀態和本地的狀態是分開的，**同步**的動作很重要!!

### Git 基本指令
先下載、安裝 [Git](https://git-scm.com/downloads) 吧，並且將 Git 加入環境變數，  
進入專案的根目錄，在 cmd 中輸入：
```
> git init
```
會發現專案中多了一個資料夾 `.git` ，它就是 git 版本資訊儲存的地方。  
接下來可以將整個數據庫複製到本地，使用 `clone` 指令會新增並追蹤該數據庫，並取名為 `origin`：

```
> git clone <repository_url>  
```
將檔案複製到本地之後，還需要取得各個分支的資訊，才能切換分支：
```
> git fetch origin
```

專案可以添加多個數據庫，要為它們取不同的名字 ( 預設是origin )，手動新增程式庫的指令如下， `-u` 參數可以追蹤該數據庫：
```
> git remote add [-u] <remote_name> <repository_url>
```
  
有了數據庫，就可以開始 coding 囉～  

最常用的指令是 `add`、`commit`、`push`，  
`add` 指令用來告訴 git 哪些檔案的變動要記錄起來， `.` 代表所有變動。
```
> git add <file_path>
> git add .   // all files
```  
`commit` 確認紀錄變動，且要附上確認訊息，明確資訊、統一格式才是好習慣。
```
> git commit -m "fix: login bugs" 
> git commit -m "ggez"   // 這樣沒人看得懂
```
`push` 更新數據庫的資訊，丟到雲端中大家都看的見，須附上數據庫還有分支的名稱。
```
> git push <remote_name> <branch_name>
```
若搞不清楚狀況，或是按錯鍵，就輸入這個超棒的指令 `status`，它會告訴你現在 git 的狀況，像是有變動尚未紀錄或是確認，以及本地版本與數據庫的版本是否相符。
```
> git status
```

### 其他 Git 指令
跟別人合作時，夥伴將程式碼 push 到數據庫後，可以用 `pull`取出最新版本的 code，每次開始 coding 前，都要記得 pull 一下，保持同步。
```
> git pull <remote_name> <branch_name>
```
對於正在追蹤的數據庫，只需要 `push`、`pull` 就可以了，省略了`remote_name` 和 `branch_name` 。  
```
> git pull
> git ...
> git push
``` 
終於輪到 `branch` 出場了，顧名思義就是分支的意思，同一個數據庫可以擁有多個分支，製作實驗性功能的時候相當好用，不需修改主幹，~~萬一 code 寫壞了，只需剪掉分支就行了。~~   
使用 `checkout` 可以切換分支，本地的 Code 也會隨之切換，加上參數 `-b` 可以建立新分支：
```
> git checkout <branch_name>
> git checkout -b <branch_name>    // add and switch to new branch
```
`branch` 則用來看看目前正處於哪一個分支，也可以建立分支。
```
> git branch  // view all branches
> git branch <new_branch_name>
```
`reset` 可以讓時光回流，主要有 `-soft`、`-mixed`、`-hard` 三種參數，一旦使用 `reset`，版本便一去不復返，只是程度的區別。  
`-soft` ~~就是說話不算話~~，會取消 `commit`，讓變動確認失效，不影響程式碼和想要更改的部分。
```
> git reset -soft <version>
```
`-mixed` ~~就如失憶~~，會取消 `add` ，讓 git 不記得有這個改動，但不會更改程式碼，若不加參數就會是以此方式進行重設。
```
> git reset <version>
```
`-hard` 會直接乘著時光機到指定版本，再當次版本之後的改動都會消失殆盡，謹慎服用。
```
> git reset -hard <version>
```
git 版本的表示方法如下 :  
  
+ `HEAD` 當前版本
+ `HEAD^` 前1版本
+ `HEAD~2` 前2版本
+ `HEAD~X` 前X版本

`stash` 指令的功能和 `reset` 有些類似，但它是讓尚未確認的更動儲存起來，並回到當前版本的樣子，方便開啟新分支進行其他改動。
```
> git stash
> git stash pop   // get stash content 
``` 
`diff` 可以用來比較兩個本版的區別
```
> git diff <version1> <version2>
```
`log` 可以查看 git 的歷史以及版本號
```
> git log
```
若要回復單一檔案至某版本，可以這樣輸入：
```
> git checkout <version> <file_path>
```
