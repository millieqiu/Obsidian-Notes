### Vue 檔案拆分 & npm 套件管理 & Webpack 打包 (Done)
1. 把 Vue 的檔案拆分 (不同功能會是不同 JS 檔)
2. 使用 Webpack 打包 JS
---
檢討：
1. 原本安裝的是 2.7.14 版本的 Vue，這版為了更好地相容 Vue3 因此引入的寫法必須跟 Vue3 一樣。
   ==解法== npm install vue@2.6.14 降到較低的版本，再重新打包一次（新的會自動覆蓋舊的）就 OK 了。

### SASS (Done)
1. CSS 替換成 Bootstrap (Ex 顏色變數等)
2. Babel loader 轉換 JS (webpack.config.js)
3. SASS loader 轉換 SASS
4. 把 JS 跟 CSS 分離開來
Webpack > 只認得 JS 檔案 (入口是JS 出口也是JS)
有個屬性可以把 JS 跟 SASS 分開

---
檢討：
1. 外部連結引入 google font 會讓造成網頁讀取的順序有不同
   先跑完 CSS 了，但字體還沒加載完，所以造成 HTML 畫面閃現

### Webpack
webpack 的 mode 設定成 development 是為了除錯方便，但不能上版用。
現有的方式只有產出一種環境，如果需要多個環境：npm run build (後面接參數或其他)
- [x] 拆成兩個環境：開發 / production
- [x] webpack watch > 監看 (如果 code 有改可以自動重新 build 一次) > development mode
- [x] 新需求：接 Web API 天氣 (網頁上需要新增欄位) (後端)
- [x] 改變數 > 換主色

Reference:
> [Production Setup @ Webpack -Guide](https://webpack.docschina.org/guides/production/)
> [Webpack 學習筆記 - PJCHENder](https://pjchender.dev/webpack/note-webpack/#%E6%AD%A3%E5%BC%8F%E7%92%B0%E5%A2%83production-mode)

---
檢討：
1. webpack 環境切換寫在同一支檔案，用 if 判斷。
   壞處：有很多 plugin 讓檔案跑起來很冗長
   好處：當配置差不多時較容易閱讀
   通常建議拆成兩個檔案寫 dev / prod


### Profile page (變更照片)
1. 沒設照片前有預設照片
2. 選擇照片、上傳前的預覽模式
3. input file 檔案類型只能選圖片 
限制檔案類別：accept="image/gif, image/jpeg, image/png"
---
檢討：
1. default 預設大頭照應該跟著被部署到伺服器上，所以適合放到 wwwroot 裡


### Loading
1. 讀檔案時：選照片的時候
   如果讀取的照片很大，會卡頓很久
   fileReader 可以做讀檔案的時候中間的動作
2. 呼 API 時
3. Header 按鈕文字變更 (設定/TODO)

1. 進度條：只能監測開始跟結束，中間的加載 % 數 (在讀取網頁時) 可能是假的 >> 較少使用
   通常會用 spinner 來表示

#### Blob


#### Vue2
new Vue ({
 data...
 methods...
})
==選項式== API

mixin (不容易發現到底放了甚麼資料進去，不易維護，即將被淘汰)

#### Vue 3
組合式 API

### Oauth 第三方
四個流程
1. 隱式：透過網址來傳遞 token (比較不安全) > 沒有 refresh token
2. 授權碼：較麻煩 授權回傳的認證是一組「認證碼」(變成其中一個參數)
   用 POST 的方式
3. 密碼：最少人使用 通常是拿來做內部系統
4. 針對系統

- [x] 解決 loading 畫面 跑板問題
- [x] Google 登入按鈕
- [x] 網頁 RWD 優化
- [ ] Webpack（圖片？）
      - google logo `<img>` 包 svg 檔
      - user avatar png/jpg/jpeg...等
      - 垃圾桶 icon `<svg>` 標籤
- [x] font-awesome icon
      將 svg 圖檔改變顏色用 `fill` 屬性
- [ ] git merge & rebase 指令
- [x] api 串接方式全部改成 fetch
- [ ] fetch 錯誤訊息 (error handling)

### Network 專有名詞
- [ ] networking queing 專有名詞
- [x] watch v.s. computed
- [x] todo list 字數限制
- [ ] 看看 api 文件長怎樣
- [ ] postman v.s. swagger

頁面跳轉方式
- href
- assign
- location

networking queing 專有名詞

要問的問題
1. max-length 如何決定
2. Bootstrap 套件問題 (現行引入方式＆瘦身處理)
3. 