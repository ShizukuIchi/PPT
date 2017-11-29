# 雲端架站 PPT ver.

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

----

![淹水](https://media.giphy.com/media/l41YcLnzt7SNyxUha/giphy.gif)

----

![窮](https://media.giphy.com/media/132pnhRx4EM7ni/giphy.gif =400x)
![意外](https://media.giphy.com/media/5Zesu5VPNGJlm/giphy.gif =400x)

---

## 雲端選擇

----

### Iass 基礎設施即服務
AMZ、DigitalOcean 提供的就是 Iass  
就像租一台主機，從基礎開始建置  
  
-> 直接用 putty 連上主機

----

### Pass 平台即服務
等等介紹的 Heroku 就是 Pass  
基礎環境設定好了，使用 API 做額外設定  

-> 安裝專屬 Cli 操作

----

### 選擇
* 通常 Pass 會比 Iass 貴
* Iass 從頭打造，彈性更高

---

## Heroku

* 免費額度
* 可和 Github 連結
* 基本功能不需綁信用卡
* 自訂 subdomain

----

## [Heroku Cli](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)

可以透過網站管理 Heroku 帳戶，不過有 Command line/shell 方便許多。  
同時安裝 [Git](https://git-scm.com/) 以及設定環境變數。

---

## Getting Started

----

檢查環境需求
```shell
$ node -v
$ npm -v
$ git --version
```

----

[**註冊**](https://signup.heroku.com/)
透過 Heroku Cli 登入帳號
```shell
$ heroku login
```

---

## 準備專案

----

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

----

建立App
```shell
$ heroku create
```
查看 remote
```shell
$ git remote
$ git remote -v
```

----

修改 App 名稱
```shell
$ heroku apps:rename new_name
```
更新 git remote
```shell
$ git remote rm heroku
$ heroku git:remote –a new_name 
```
針對某 App 執行操作
```shell
$ heroku apps:rename -a=app_name new_name
```

---

## 部屬檔案囉

----

檔案上傳
```shell
$ git push heroku master
```
確認執行核心
```shell
$ heroku ps:scale web=1
```

----

開啟 App
```shell
$ heroku open
```
下班
```javascript
It works!
```

---

## 基本設定

----

設定 Procfile  
告訴 Heroku 主機如何執行 server
```=
web: node index.js
```
暫停使用
```shell
$ heroku ps:scale web=0
```

---

## 檢查狀況

----

查看 log
```shell
$ heroku logs [--tail]
```
查看 App 狀況
```shell
$ heroku ps
```

---

## 小試身手

----

修改檔案
```htmlmixed=
// index.js

...

app.get('/hello', function(req, res){
  res.send('olleh');
})

...
```

----

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

----

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

----

執行 node
```shell
$ heroku run node
```
執行 shell
```shell
$ heroku run bash
```
※ 退出 shell
```shell
$ exit
```

---

## `.env` 環境變數

----

本地端 debug 的時需要`.env`
```=
// .env

NAME=Ting
```
加入 `.gitignore`
```=
// .gitignore

...
.env
```

----

Heroku server
```shell
$ heorku config:set NAME=Ting
```
查看變數
```shell
$ heroku config
```

---

## 自己動手來

----

1. 專案加入 Git 
2. 建立 Heroku App
3. 設定 Git remote、App 名稱
4. 新增 `Procfile`
5. 部屬至 Heroku

※ `process.env.PORT`

---

## [Form 資料傳輸格式](https://www.w3.org/TR/html401/interact/forms.html#h-17.13.4)

----

### application/x-www-form-urlencoded

```htmlmixed=
<form action="url" method="post">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <input type="submit" value="送出" />
</form>
```

----


```htmlmixed
Content-Type: application/x-www-form-urlencoded;charset=utf-8

username=%E5%B9%B9&password=123
```

----

### multipart/form-data
```htmlmixed=
<form action="url" method="post" enctype="multipart/form-data">
    <input type="file" name="file" />
    <input type="text" name="comment" />
    <input type="submit" value="上傳" />
</form>
```

----

```htmlmixed
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

----

### 有啥區別呢？
`application/x-www-form-urlencoded`  
還是能夠傳輸檔案的  
但須以三倍的空間儲存資訊 如：`!` -> `%21`  

----

### 那都用 multipart/form-data 就好啦！
當資料簡單時
[MIME](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_types) 反而較沒有效率

----

## 其他常用 POST 資料格式

----

### application/json
以 Json 格式傳送資料，在字串與 Json 物件間轉換簡單，趨向主流

----

### text/plain
Fetch 預設使用 `text/plain`
除了 spaces 之外不進行編碼

----

## 傳遞陣列 ?

----

想像下列情況：
* 不確定資料筆數
* 需任意刪減欄位
* 同性質多筆資料

----

Server 直接處理
```htmlmixed=
<input type="text" name="fruit[]">
<input type="text" name="fruit[]">
<input type="text" name="fruit[]">
```

----

傳送 JSON
```javascript=
{ 
  name: 'piko',
  fruit:  ['pen', 'pineapple', 'apple']
}
 ```

----

直接這樣
```htmlmixed=
<input type="text" name="fruit" value="apple"> 
<input type="text" name="fruit" value="pen">

// fruit=apple&fruit=pen
```

----

## npm [qs](https://github.com/ljharb/qs)
```javascript=
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

## 團隊合作

----

### 物件變數名稱
* 書 -> book: object
* 借出狀態 -> ~~status~~ isBorrowed: bool
* 書號 -> id: uniq string
* 書名 -> name: string 

----

```javascript=
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

----

### Git commit style
```shell
// good
$ git commit -m 'add: login view'
$ git commit -m 'del: change color button'

// bad
$ git commit -m 'bugs fixed'

// very bad
$ git commit -m 'e04都我在做'
```

----

### Git 大冒險 : 穿越時空
* 支線任務
* 回朔
* ~~抓戰犯~~

----

### git stash
儲存變更，回到上個版本
```shell
$ git stash
HEAD is now at 1d030b1 add doge bg
$ git checkout branch_B
```

----

查看庫存
```shell
$ git stash list
```
pop 最新的 stash
```shell
$ git stash pop
```

----

拿回來
```shell
$ git stash apply
```
拿更之前的
```shell
$ git stash apply stash@{3}
```

----

### 修改 git commit message

----

假設有三個 commits
```shell
$ git rebase -i HEAD~3
```
會出現 vim 編輯畫面
```=
pick 0952a9c message 1
pick f931e27 message 2
pick a5d8ca2 message 3

# Commands:
# ...
```

----

* pick = 不變
* reword = 修改 commit message
* fixup = 合併至前個 commit
```=
pick 0952a9c message 1
fixup f931e27 message 2
fixup a5d8ca2 message 3
```

----

開始合併
```shell
Successfully rebased and updated refs/heads
```
看看 `log` 有什麼變化吧！
```shell
$ git log
```

----

### git diff

----

與前一版
```shell
$ git diff HEAD~1 
```
某二版
```shell
$ git diff HEAD~2 HEAD~3
$ git diff HEAD~3 HEAD~2 // not same
```
使用版本號
```shell
$ git diff bf7eb80fdd48e04e04c1a5996a3505cbab1011e2
```

---

## Coding style

----

![wtf](https://media.giphy.com/media/11ahZZugJHrdLO/giphy.gif =500x)

----

### [Eslint](https://eslint.org/)


使用 npm 安裝：
```shell
$ npm install eslint --save-dev

// or globally

$ npm install eslint -g
```

----

再來一份規則套餐`.eslintrc`

```javascript=
// .eslintrc

{
    "env": {
        "browser": true,
        "node": true,
        "es6": true
    },
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
        
    }
}
```

----

### [EditorConfig](http://editorconfig.org/)
EditorConfig 需搭配 IDE 使用
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

----

優點：
* IDE 內安裝 EditorConfig 插件就能使用
* 使用簡單、直接修改 code
* 同時使用多個設定檔

----

無論如何，對於 code 的**觀感**是第一優先  
不是越短越好，而是越容易理解越好 

----

### 回頭整理

----

![](https://i.imgur.com/SkcoyYG.png =500x)

----

### 請人 debug

----

![](https://i.imgur.com/SkcoyYG.png =700x)

----

### 找 bug

----

![](https://i.imgur.com/SkcoyYG.png =1000x)

---

## 小結語
* 不要僥倖  
* 學好學滿  
* 不進則退

---

<span style="font-size: 200px;">3Q</span>