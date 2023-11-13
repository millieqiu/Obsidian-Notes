# Day 1
## 透過 Leetcode 學習 TS
> [共筆連結]()


# 哇嗚，原來 Vue.js 還能這樣寫！
### component & template
`.define` 取代 `.mount`

### inline v-for in Array & Object
不用因為三五行的選項再另外用一個函式來引入

用 checkbox 實現單選
`:true-value` & `:false-value`

### Pass function as props
`ref` 是 Vue 的特性，用來呼叫元件綁定的實際 DOM

defineExpose 最好只拋出去一個 function，讓元件的狀態在哪裡，資料就在哪裡，比較好做後續的管理
大部分的情況下，還是推薦用 `props` 跟 `emit` 去做元件間的溝通管理

在 slot 狀態下若要讀取元件的狀態，用 `MutationObserver` API

Render Function > 在開發套件時較常使用

vapor mode

---

# Day 2

## 模組化前端開發：從亂七八糟到組織有序
Vite 不是 Vue 專屬的，也不是打包工具

esbuild <- Vite -> Rollup

`type="importmap"`
類似 CDN，但==不需要打包==，擺脫 node_modules
