取值使用 getElementById 替換掉 >> Vue
使用框架的好處：雙向綁定
>雙向綁定：在表單的輸入元素上 (input, select, textarea) 跟資料進行綁定

在 Vue3 也有為 v-model 增添不一樣的屬性，例如 `v-model.trim` 可以去除前面的空白字元； `v-model.lazy` 可以在輸入完畢才會將內容儲存起來，換句話說就是將游標跳出，`input` 輸入框才會將值寫入到變數內。

v-model

Udemy 2-5節
Hiskio 3-10節
xw2561@gmail.com
2351. (公司)

替換 API 的方法 (不使用jQuery)
1. Fetch.js
2. axios (公司較常用)

---

# Vue.js
## MVVM 架構
Model         ↔       View Model        ↔       View
 ^^^                                ^^^                            ^^^
Vue實例的data          Vue 實例                     DOM

1. Vue 模板 (v-for, v-model, v-if 等)
   如何把資料跟 DOM 做連結
2. Vue 實例
   利用 `new Vue` 宣告一個 view model
3. Vue 組件
   把模板、實例跟 CSS 放在同一個檔案裡，方便開發與管理。
   - common js 語法
   - 用 webpack 打包

Vue 是**聲明式**渲染，先宣告元素的 id。
如果是 jQuery 就是命令式渲染，一個口令一個動作的程式寫法。

## 指令
- v-text：更新元素的 textContent
- v-html：更新元素的 innerHTML
- v-bind：把資料綁定到 DOM 上
- v-on：接收 (監聽) DOM 的事件來改變資料

## 模板 (template)
template 裡的資料是字串，可以作為畫面上要 render 出來的模板，描述畫面的長相。

## methods
物件裡面的屬性為「函式」。
1. data 裡的命名跟 methods 的命名不能一樣
2. methods 的函式不能宣告成箭頭函式，因為在函式裡經常用到 `this`，且箭頭函式的 this 會指向父層 (window)

## 類別與實例
類別：用來描述一個東西的屬性跟方法 Ex: 有濃眉大眼，建立在「人類」這個 class 裡面
實例：


## 計算屬性 (computed) v.s. 偵聽器 (watch)

### computed
與 methods 相似，裡面的屬性是一個**函式**，但 computed 裡面的函式一定要 `return` 一個值，代表計算結果。
computed 的屬性也可宣告為「**物件**」，其中有兩個方法分別為 get() 與 set()。
#### 特點
- 當元件被創建時（created 生命週期），computed 函式會被建立和執行一次。之後如果依賴沒有更新，就不會重新執行和求值，而是回傳之前緩存起來的值。
- computed 的值只能被該 computed 函式修改，不能被其他方法修改，例如 `this.某computed 函式 = 123` 會報錯。
- computed 的函式必須要**回傳一個值**。
- computed 的函式無法傳入參數。

看看 Vue 官方執行 computed 的解釋：
```text
计算属性是基于它们的响应式依赖进行缓存的。只在相关响应式依赖发生改变时它们才会重新求值。
```
什麼是響應式依賴？意思是在一個 computed 函式裏，它所用到在 **`data` 建立的資料**。  
一旦這些資料有變化，這個 computed 函式就會被重新執行和求值。


### watch
型態為物件，可以宣告函式。
會偵聽 data, computed 的變動。
【進階用法】
先將型態設定為物件，在物件中新增 `handler` 函式（效果與直接設定函式型態相同），以及兩個額外屬性：
- `immediate`
  預設 watch 的函式需要等待它所偵測的值變動時，才會執行。但如果想一載入元件就執行，可以設定 `immediate: true`，如此一來在 Vue 初始化的時候就會進行偵聽。
- `deep`
  當要偵測物件裏的屬性的變動時，需使用 deep: true。Ex: 若屬性為物件或陣列時。

#### 特點
- watch 會偵測某個值，當該值有變化時，就會執行。
- watch 可傳入參數，第一個參數是更新後的值，第二是舊值。
- 比起 computed，可以處理非同步工作。

## 生命週期
如同生物一般，Vue 的實體物件從建立、掛載、更新、銷毀移除，這一連串的過程就稱為「生命週期」。在這些過程中，Vue.js 提供了開發者在這些週期階段做對應處理的 callback function，我們便稱之為生命週期的 hooks function。
![[vue-lifecycle.png]]

### 使用方式與時機
在 Vue 實體裡直接加入對應名稱的 hook function，就可以在進行至不同生命週期階段時，自動觸發該函式。
```
⭐ 提醒：hook function 不能加在 methods 裡面，且須透過 this 存取實體，因此與 methods 一樣無法使用箭頭函式。
```

Vue 實體從建立、掛載到渲染至瀏覽器畫面上，會經歷這幾個階段：`beforeCreate`、`created`、`beforeMount`、`mounted`。
-  `beforeCreate`：Vue 實體剛被建立，狀態與事件尚未初始化，此時還無法取得 data、methods、computed 等資料。
- `created`：實例創建完成，可訪問 data、methods、computed 等方法和數據，但**元素還未掛載到 DOM 上**，不能訪問 el 屬性。
- `beforeMount`：
- `mounted`：到此階段，Vue.js 正式將網頁上的 DOM 節點及事件綁定到 Vue 實體，常用來導入初始的 ajax code，是較常使用的函式。


---

Vue.js - 表單驗證實作
使用 watch 偵聽器
> [Using watchers for form input validation in Vue.js](https://devpress.csdn.net/vue/62f4ba2e7e668234661888b6.html)

computed 計算屬性
追蹤的對象是自己定義的資料

**watch v.s. computed**
watch 的效能比較差
computed 會 return 一個值

==表單驗證的方式==
1. 寫在 HTML 裡面
2. 寫在 Vue 即時偵測
實務上會採取**即時回饋**的方式，方便 user 知道哪裡有錯及修改。
用 HTML 內建的，因為各瀏覽器的樣式不同，難以達到一致的設計風格，雖然方便但較沒有彈性。

`computed` 最大特點是必須回傳一個值，並且會把它緩存起來，當函式裏的依賴改變時，才會重新執行和求值。`watch` 則不強制要求回傳一個值，取決於 user 需不需要用到。
watch 會偵測**單一個值**，當它有變化時就執行。


# Vue - component
