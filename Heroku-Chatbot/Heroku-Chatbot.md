# 雲端架站 PPT ver.

[Shizuku](https://www.facebook.com/shizuku.ichi)@CNA

---

## About me

* 資管四
* 喜歡將程式融入生活中，讓生活更優雅(?
* 略懂 Python 
* 但今天用的是 Javascript

---

## 讓你聽聽

* Git 版本控管
* 雲端架站
* Heroku
* 雲端部屬
* FB Chatbot 實作

---

## [Git 版本控管](https://github.com/ShizukuIchi/before-react-native/blob/master/Git.md)

----

## 基本指令介紹

+ clone/init
+ remote
+ add/commit
+ push/pull

----

### 範例 1
```shell
// 從網路下載程式碼
$ git clone https://XXX.git
// 修改檔案 a.txt 並確認 a.txt 的變更
$ git add a.txt
// 儲存變更(本地端)
$ git commit -m "bug fixed"
// 將修改後的程式碼上傳
$ git push origin master
```

----

### 範例 2
```shell
// 寫了好多程式
$ git init
// 所有檔案變更加入追蹤
$ git add .
// 儲存變更(本地端) 
$ git commit -m "bug fixed"
// 設定上傳的地址
$ git remote add origin https://XXX.git
// 上傳至網路
$ git push origin master
```

---

## 雲端架站

----

![淹水](https://media.giphy.com/media/l41YcLnzt7SNyxUha/giphy.gif)

----

![窮](https://media.giphy.com/media/132pnhRx4EM7ni/giphy.gif)

---

![意外](https://media.giphy.com/media/5Zesu5VPNGJlm/giphy.gif)

---

## 雲端選擇

----

### Iass 從頭來
AMZ、DigitalOcean 提供的就是 Iass  
就像租一台主機，從基礎開始建置  
  
-> 遠端連上主機操作

----

### Pass 包好好
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

今天先不用

---

## Getting Started

----

[**下載 Git**](https://git-scm.com/download/)
檢查環境需求
```shell
$ git --version
```

----

## 擁有 Heroku

----

1. [**註冊 Heroku**](https://signup.heroku.com/) (語言選 Nodejs, 需驗證 email)
2. [**建立 Heroku App**](https://dashboard.heroku.com/apps)
3. 取個喜歡的 App 名稱



----

## 下載範例程式碼

----

> $ 部分皆在 Git cmd 框框內操作

抓檔案
```shell
$ git clone https://github.com/heroku/node-js-getting-started.git
```
進入資料夾
```shell
$ cd node-js-getting-started
```

----

設定程式碼上傳的地方
```shell
$ git remote add heroku https://git.heroku.com/你的App名稱.git
$ git remote -v
```

**※不准直接給我打"你的App名稱"進去**

---

## 上傳檔案囉

----

檔案上傳至 Heroku
```shell
$ git push heroku master
```
稍等...

開啟網址
```shell
https://你的App名稱.herokuapp.com/
```

----

## 下課!

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
```javascript=
// index.js

express()
  .use(express.static(path.join(__dirname, 'public')))
  .set('views', path.join(__dirname, 'views'))
  .set('view engine', 'ejs')
  .get('/', (req, res) => res.render('pages/index'))
  .listen(PORT, () => console.log(`Listening on ${ PORT }`))

```

----

貼心提醒: 第8行
```javascript=
// index.js

express()
  .use(express.static(path.join(__dirname, 'public')))
  .set('views', path.join(__dirname, 'views'))
  .set('view engine', 'ejs')
  .get('/', (req, res) => res.render('pages/index'))
  .get('/hello', (req, res) => res.send('olleh'))
  .listen(PORT, () => console.log(`Listening on ${ PORT }`))
```

----

上傳試試
```shell
$ git commit -am 'hi'
$ git push heroku master
```

開啟網址
```shell
https://你的App名稱.herokuapp.com/hello
```

---

## 敏感資訊?

----

有些資訊直接寫在程式碼裡面不太OK
可在 Settings > Config Variables 設定
![](https://i.imgur.com/IJjYuFA.png)

Heroku 以 `process.env.name` 取得 value

---

## 實作 FB Chatbot!

----

1. 下載 [zip檔案](https://github.com/ShizukuIchi/my-chatbot/archive/master.zip) 至剛剛的資料夾
2. 建立 Heroku App 並取名

----

3. 使用 git 上傳至heroku
```shell
$ git init
$ git add .
$ git commit -m "first commit"
$ git remote add heroku https://git.heroku.com/你的App名稱.git
$ git push heroku master
```

----

3. [建立FB應用程式](https://developers.facebook.com/apps/)
    * 成為 FB App 開發人員
    * 新增應用程式 (Messenger)

4. 往下拉到權杖產生
    * 建立粉絲專頁 (休閒娛樂)
    * 選擇剛創立的粉專
    * 建立並複製產生的一大串英數字

----

5. 設定webhook
![](https://i.imgur.com/og5MYE2.png)

----

6. 訂閱創立的粉絲專頁

7. 將權杖放入 Heroku Config
![](https://i.imgur.com/W8ln52D.png)

----

8. [驗證權杖](https://www.hurl.it/)
右邊格子填入 https://graph.facebook.com/v2.6/me/subscribed_apps?access_token=權杖
![](https://i.imgur.com/RkN7wtp.png)

----

9. 開始測試吧!!!!
![](https://i.imgur.com/jwkx7Oa.png)

---

## Q_Q & A_A

