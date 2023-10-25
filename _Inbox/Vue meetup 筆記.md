# 簡報
- Slidev
  基於 Vue 及 Vite 的投影片工具（可 markdown 語法）
  
可以使用 unocss：
https://unocss.dev/

VueUse 封裝簡報做動態效果
RecordRTC.js

使用 npm 安裝（node.js 18 以上）

以往只能用圖片顯示程式碼，用工具則可以直接打程式碼

特色：
1. Components
   Ex: 箭頭、Tweets Components 引用別人的文章
   自定義 Components 可以製作類似計數器的元件，就能直接在簡報裡點擊 demo
2. Code：呈現程式碼，可高亮呈現
   引入編輯器（Ex: 將程式碼重構後，要指出兩段程式碼之間的差異，可使用 `monacoDiff` 編輯器，在程式碼區塊直接宣告即可使用）
3. Animation
   用 `v-click` 操作，宣告陣列，可在特定的點擊數達到指定的動畫效果
   `v-motion` 
4. 螢幕錄影
   簡報內建 Recording 效果
   可以選擇攝影機、輸出格式、輸入麥克風音源
5. Export
   playwright.chromium 套件
   用指令來指定輸出簡報的檔案格式（PDF、png等）

優勢：
1. HMR 即時更新
2. 高亮程式碼區塊
3. 主題樣式＆彈性客製化

