# 雲端架站&合作效率

楊楚玄

---

## About me

* 資管四
* 喜歡將程式融入生活中，讓生活更優雅(?
* 略懂 Python 
* 用過一點點 React

---

## 讓你聽聽

* 雲端架站
* Heroku
* 雲端部屬
* 實際應用
* 資料格式
* 合作效率

---

## 雲端架站

* 窮
* 天災
* 專精技能點

---

## 雲端選擇

### Iass 基礎設施即服務
AMZ、DigitalOcean 提供的就是 Iass  
就像租一台主機，從基礎開始建置  
  
-> 直接用 putty 連上主機

### Pass 平台即服務
等等介紹的 Heroku 就是 Pass  
基礎環境設定好了，使用 API 做額外設定  

-> 安裝專屬 Cli 操作

### 選擇
* 通常 Pass 會比 Iass 貴
* Iass 從頭打造，彈性更高

---

## Heroku

* 免費額度
* 可和 Github 連結
* 基本功能不需綁信用卡
* 自訂 subdomain

---

## [Heroku Cli](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)

可以透過網站管理 Heroku 帳戶，不過有 Command line/shell 方便許多。  
同時安裝 [Git](https://git-scm.com/) 以及設定環境變數。

---

## Getting Started
* [註冊](https://signup.heroku.com/)
* 檢查環境需求
```shell
$ node -v
$ npm -v
$ git --version
```
* 透過 Heroku Cli 登入帳號
```shell
$ heroku login
```

---

## 準備專案
抓檔案
```shell
$ git clone https://github.com/heroku/node-js-getting-started.git
```
進入資料夾
```shell
$ cd node-js-getting-started
```

---

## Heroku App
建立App
* 自動建立 remote -> heroku
* 還有怪怪的 App 名稱

```shell
$ heroku create
```
查看 remote
```shell
$ git remote
$ git remote -v
```
修改 App 名稱
```shell
$ heroku apps:rename new_name

// 若在其他地方修改 App 名稱需要更新 remote
$ git remote rm heroku
$ heroku git:remote –a new_name 
```
針對某 App 執行操作
```shell
$ heroku apps:rename -a=app_name new_name
```

---

## 部屬檔案囉
檔案上傳
```shell
$ git push heroku master
```
確認執行核心
```shell
$ heroku ps:scale web=1
```
開啟 App
```shell
$ heroku open
```
下班(？

---

## 基本設定

設定 Procfile，告訴 Heroku 主機如何執行 server
* web: 加入 router 接收流量
* worker: 僅工作
```
// Procfile

web: node index.js
```
暫停使用
```shell
$ heroku ps:scale web=0
```

---

## 檢查狀況
查看 log
```shell
$ heroku logs [--tail]
```
查看 App 狀況
* 使用中的核心
* 剩餘時數
```shell
$ heroku ps
```

---

## 小試身手
修改檔案
```htmlmixed
// index.js

...

app.get('hello', function(req, res){
  res.send('olleh');
})

...
```
本地端試跑
```shell
$ heroku local web 
```
上傳試試
```shell
$ git push heroku master
$ heroku open hello
```

---

## Heroku 插件

Heroku 提供許多好用的插件
不過有些就算免費，也可能需要綁信用卡
可至網頁管理介面看看價格方案

加入插件
```shell
$ heroku addons:create XXX
```
確認有哪些插件
```shell
$ heroku addons
```
查看插件
```shell
$ heroku addons:open XXX
```

---

## 身歷其境
在 Heroku 上執行 node
```shell
$ heroku run node
```
在 Heroku 上執行 shell
```shell
$ heroku run bash
```
※ 執行 shell 後記得退出，不然會占用核心時數
```shell
$ exit
```

---

## 設定 `.env` 環境變數檔
使用資料庫等等含有帳戶信息的東西就需要設定

在本地端 debug 的時候要新增 `.env` 檔：
```
// .env

NAME=Ting
```
含有重要資訊，所以會加入 `.gitignore`
```
// .gitignore

...
.env
```
Heroku server 的環境變數怎麼設呢？
```shell
$ heorku config:set NAME=Ting
```
查看設了哪些變數
```shell
$ heroku config
```
 
---

## 自己動手來
1. 專案加入 Git 
2. 建立 Heroku App
3. 設定 Git remote、App 名稱
4. 新增 `Procfile`
5. 部屬至 Heroku

※ 上線的 Port 是由 Heroku 設定，須給 `process.env.PORT    `
 
---

## [Form 資料傳輸格式](https://www.w3.org/TR/html401/interact/forms.html#h-17.13.4)
> 送出資料時須注意格式，否則會有意想不到的錯誤  
> 傳輸檔案有編碼問題，在此不提

Request header 中的 Content-Type 代表資料格式
HTML Form 使用以下前兩者之一傳送資料

### application/x-www-form-urlencoded
預設格式 -> 其實就是送出一段字串  
以`+`取代空格、`=`區隔名稱和值、`&`區隔欄位  
  
範例：
```htmlmixed
<form action="url" method="post">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <input type="submit" value="送出" />
</form>
```
送出的東西：
```
Content-Type: application/x-www-form-urlencoded;charset=utf-8

username=%E5%B9%B9&password=123
```
除了英文數字，都會被轉為`%GG`的樣子，用 ASCII code 來表示  

### multipart/form-data
上傳內容帶有檔案時，就必須使用此格式  

```htmlmixed
<form action="url" method="post" enctype="multipart/form-data">
    <input type="file" name="file" />
    <input type="text" name="comment" />
    <input type="submit" value="上傳" />
</form>
```
送出的東西：
```
Content-Type: multipart/form-data; boundary=GG3b0

--GG3b0
Content-Disposition: form-data; name="file"; filename="pa.jpg"
Content-Type: image/jpeg

... contents of pa.jpg ...
--GG3b0
Content-Disposition: form-data; name="comment"

jieyiwolaopola!!
--GG3b0--
```
以`boundary`區隔欄位，不編碼  
每個欄位可以再填入`Content-Type`，表示檔案類型

### 有啥區別呢？
`application/x-www-form-urlencoded`還是能夠傳輸檔案的  
但須以三倍的空間儲存資訊 如：`!` -> `%21`  
  

### 那都用 multipart/form-data 就好啦！
當資料簡單時 (如：登入表單)
[MIME](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_types) 反而較沒有效率

---

## 其他常用 POST 資料格式


### application/json
以 Json 格式傳送資料，在字串與 Json 物件間轉換簡單，趨向主流
[RESTful API](http://www.restapitutorial.com/) 幾乎都使用此格式
### text/plain
Fetch 預設使用 `text/plain`
較少用，與`application/x-www-form-urlencoded`類似
但除了 spaces 之外不進行編碼

---

## 傳遞陣列 ?

想像下列情況：
* 不確定資料筆數
* 需任意刪減欄位
* 同性質多筆資料
  
讓 Server 端以接收陣列訊息，直接以`fruit[n]`取得各個 fruit 的值：
```htmlmixed
<input type="text" name="fruit[]">
<input type="text" name="fruit[]">
<input type="text" name="fruit[]">
```
    
或是直接傳送 JSON，兩端處理一下物件和字串的轉換：
```javascript
{ 
  name: 'piko',
  fruit:  ['pen', 'pineapple', 'apple']
}
 ```
其實還可以直接這樣傳送：
```htmlmixed
<input type="text" name="fruit" value="apple"> 
<input type="text" name="fruit" value="pen">

// fruit=apple&fruit=pen
```
但 server 端就要特別處理了。

---

## npm [qs](https://github.com/ljharb/qs)
將網址後的 query string 轉為 json
```javascript
const qs = require('qs');
const url = 'https://www.test.com?name=ting&gg=yy'

let myJson = qs.parse(url.split('?').pop())

// myJson
/**
 * {
 *   name: 'ting',
 *   gg: 'yy' 
 * }
 */

```

---

## 物件變數名稱
以圖書系統為例
* 書 -> book: object
* 書單 -> ~~bookPaper~~ bookList: array[books]
* 借出狀態 -> ~~status~~ isBorrowed: bool
* 書號 -> id: uniq string
* 書名 -> name: string 
 
光看變數名稱就能知道變數型態
```javascript
book {
  id: '3',
  uid: 'n12ku0w98jf928jfmi2f9j2f',
  name: 'Hello World!',
  isBorrowed: true,
}

category {
  name: 'happy',
  bookList: array[books],
}
```

---

## Git commit style
> 好的 commit 習慣，提升團隊 coding 效率和氣氛 
> 壞的 吵架拆夥自己寫自己的都有

團隊擬個 commit 格式  
不用查看修改的內容，就能知道改了甚麼東西
```shell
// good
$ git commit -m 'add: login view'
$ git commit -m 'del: change color button'

// bad
$ git commit -m 'bugs fixed'

// very bad
$ git commit -m 'e04都我在做'
```


---

## Git 大冒險 : 穿越時空
* 支線任務
    * 開寫實驗性功能時，可以新增一個 branch
      不影響主線任務的進行，完成時再 merge 回 master
* 回朔
    * 莫名其妙就爆炸了，想起當初美好的時光
      已經浪費太多時間了，回去吧！ ~~Git就是這樣用的~~
      但要注意別太衝動，操作時光是有風險的
* ~~抓戰犯~~

---

## Git 起來

熟悉 git 的基本功能還不夠  
有時會需要一些更厲害的指令  
以下介紹一些 hen 棒的指令  

## git stash

有時在 branch A 工作到一半，突然需要至 branch B 處理其他 code
可使用 `git stash` 儲存變更，並回復到上個 commit 的狀態
接下來就能直接切換到另一個 branch
```shell
$ git stash
HEAD is now at 1d030b1 add doge bg
$ git checkout branch_B
```

### git stash apply
想要拿回儲存的 code 可以先看看倉庫放了些什麼：
```shell
$ git stash list
```

拿回來：
```shell
$ git stash apply
```
拿回更之前的：
```shell
$ git stash apply stash@{3}
```
pop 最新的 stash
```shell
$ git stash pop
```

---

## git rebase

`rebase` 跟 `merge` 很像，但後者單純合併兩個 branch 的最新版本，前者則是從分支點一版一版修正衝突，完成後分支樹就只剩一個 branch

這個，~~太麻煩了~~今天先不教，這邊教使用 `rebase` 合併 commits
連續的 commit 若是解決同一個問題可以將其合併，讓 log 更乾淨

**※** *注意不要每完成一次 commit 就 push 一次，一旦 push 了大家都看的到，再進行 rebase 就會發生怪怪的事情*

---

## git rebase -i

假設有三個 commits，輸入：
```shell
$ git rebase -i HEAD~3
```
會出現 vim 編輯畫面：
```
pick 0952a9c message 1
pick f931e27 message 2
pick a5d8ca2 message 3

# Commands:
# ...
```
決定每個 commit 的去留：
pick = 不變
reword = 修改 commit message
fixup = 合併至前個 commit
(還有很多...)

先按一下 `i`，開始修改 `rebase` 要做的事：
```
pick 0952a9c message 1
fixup f931e27 message 2
fixup a5d8ca2 message 3
```
再按 `Esc` `:` `w` `q` `Enter` 開始合併：
```
Successfully rebased and updated refs/heads
```
看看 `log` 有什麼變化吧！
```shell
$ git log
```

---

## git diff
用來查看前一版本與當前版本的差異
```shell
$ git diff HEAD~1 
```
也可以比較某二版本的差異
```shell
$ git diff HEAD~2 HEAD~3
$ git diff HEAD~3 HEAD~2 // not same
```
或是直接使用版本號
```shell
$ git diff bf7eb80fdd48e04e04c1a5996a3505cbab1011e2
```

---

## Coding style
> 瞭解別人的 code 是件難事，~~髒兮兮更是地獄~~

合作時若能統一 coding style  
對心理、生理都是一大救贖，在職場上更是無往不利。  

在此推薦完整看過一遍 [airbnb js](https://github.com/airbnb/javascript)

---

## [Eslint](https://eslint.org/)
Eslint 搭配 webpack 或 IDE 能夠及時檢查所有檔案
讓所有不符格式的 code 都跑出紅色大波浪
還可設定儲存更正語法、未修正無法上傳等等

使用 npm 安裝：
```shell
$ npm install eslint --save-dev

// or globally

$ npm install eslint -g
```
再來一份規則套餐`.eslintrc`，內容大致上有：
### Environment 環境變數
使用 Eslint 常常會加入一條規則 `no-use-before-define`   
用到未定義的變數就會報錯
* env
設定 `env` 讓 Eslint 知道有那哪些環境變數  
有 `browser`、`node` 等等環境可以直接使用

* globals
設定額外的全域變數
不過有了`env`基本上不太需要`globals`

### Parser 解析器
Parser 負責解析語法，針對使用的語法決定 Parse 如何設定
但也會跟 `env` 相互影響
* parserOptions
對解析器做額外的設定
```javascript
{
    "parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true,
          "impliedStrict": true
        }
    },
  ...
}
```

* parser
直接指定 parser，預設為 `esprima`  
可再透過 `parserOptions` 調整
```javascript
{
    "parser": "babel-eslint",
    ...
}
```
### Rules 規則
決定語法規則，犯規時該警告或是提醒  
最棒的是可以安裝規則套件，針對使用的 framework 掃描語法
* plugins
透過 npm 安裝額外的規則套件
可以在 `extends`、`rules` 裡頭使用

* extends
主要使用的規則集

* rules
設定額外的規則，優先於 `extends`

### 簡單範例 
```javascript
// .eslintrc

{
    "env": {
        "browser": true,
        "node": true,
        "es6": true
    },
    "parser": "babel-eslint",
    "extends": "eslint:recommended",
    "rules": {
        "indent": [
            "error",
            4
        ],
        "no-console": [
            "error", 
            { "allow": ["log"] }
        ],
        "no-use-before-define": 0
    }
}
```

---

## [EditorConfig](http://editorconfig.org/)
EditorConfig 需搭配 IDE 使用，以 `.editorconfig` 設定規則，可以有多個設定檔，直到遇到 `root = true` 才會停止搜尋。  
越近的規則優先度越高，`[ ]`內代表針對的檔名如 `*.py`、`*.js`
```javascript
// .editorconfig

root = true

[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
end_of_line = lf
```
優點：
* IDE 內安裝 EditorConfig 插件就能使用
* 使用簡單、直接修改 code
* 同時使用多個設定檔

---

## 我對 Coding Style 的看法
無論如何，對於 code 的**觀感**是第一優先  
不是越短越好，而是越容易理解越好 

有時只是想炫技，或是純粹想偷懶  

兩個禮拜後肯定
![](https://i.imgur.com/SkcoyYG.png)

一開始可能會有陣痛期，但是：
* 回頭整理 -> 十倍時間
* 接手 code -> 十倍時間
* 請人 debug -> 十倍時間
* 找 bug -> 十倍時間
  
還不養好習慣嗎？

---

## 小結語
* 不要僥倖  
* 學好學滿  
* 不進則退

---

<span style="font-size: 30px;">3Q</span>