# 訂正項目
form 標籤裡的 action 為空的時候會送表單到畫面本身 (欄位的資料會跑到網址裡)
form 裡面的第一個 btn 預設會當作「submit」
btn 裡面的 onclick 呼叫 api
當沒有設定 btn 的 type 時就會觸發兩個動作，一個是呼叫 api 一個是 submit
```
解決方法：
把 submit 的動作覆蓋掉 - js event prevent
移除按鈕的 onclick，在 form 上設定 onsubmit=onClickLoginOrRegister(event)
event 參數會把原本預設的動作覆蓋掉
```

計算頁數問題：使用 Math.ceil 數學函式

`.NET Core Extension Pack`

【HTML】
重複使用到的區塊可以搬到 Layout 裡面
Todo_page 的 header 有多一個登出按鈕
@User.Identity.Name >> 告訴我們目前登入的人是誰
@User.Identity.IsAuthenticated >> 目前登入的人是否有經過身分認證 (回傳布林值)
**Razor page 的語法最前面開頭加 @ 就好**

label 標籤 的 for 屬性連到 input 標籤的 id 屬性，可以直接 focus 到指定的位置

==ask: Register_page 目前可以直接輸網址進來 要擋掉==

確認密碼欄位：用 onchange 就會有順序問題 (只會偵測改變)
例如先填確認密碼的欄位再填第一個密碼欄，確認密碼欄位的錯誤訊息不會消失
解決方法：第一個密碼欄也要設定 onchange

todolist 容器預設是空白的，如果用戶沒有任何資料就會顯是一片空白
解決方法：做一個尚未有任何資料的畫面

轉址用 window.location.replace('')
換頁有兩個方法 href 跟 replace，通常用 href 居多
replace 使用情景為不應該重複觸發的頁面，可以直接取代掉 EX: 金流付錢頁面，付完款後可以 replace 回到原本的頁面

- [x] to-do: promise
- [x] to-do: eventListener

在 js 裡面寫 html 容易被判斷成惡意內容

==ask: onclick() & eventListener click ==

Email 格式的錯誤訊息：
Rubular.com 可以驗證格式下的對不對 (能不能有效判斷)


append 到 .html() 裡面有資安的風險 > 盡量不要使用
替代方案：渲染迴圈的行為 v-for

# 預習
## Promise *(待補充)*
Promise 本身是用來改善 JavaScript **非同步**的語法結構。
Promise 的三種狀態：
- Pending：尚未得到結果
- Resolved：事件已經執行完畢且成功操作，回傳 `resolve` 的結果
- Rejected：事件已經執行完畢但操作失敗，回傳 `rejected` 的結果
上列的三種狀態每次執行必定會經過 Pending，接下來進入 Fulfilled 或 Rejected 的其中之一，並且可以使用 `then()` 及 `catch()` 取得成功或失敗的結果。

>[JavaScript 中的 Promise 是什麼？以及為什麼你要懂 Promise](https://israynotarray.com/javascript/20211128/2950137358/)
>[JavaScript Promise 全介紹](https://www.casper.tw/development/2020/02/16/all-new-promise/)

## EventListener
當監聽的事件發生時，瀏覽器會去執行我們透過 `addEventListener()` 註冊的 Event Handler ([EventListener](https://developer.mozilla.org/zh-TW/docs/Web/API/EventListener)) ，也就是我們所指定的 `function`。
這個時候，EventListener 會去建立一個「事件物件」 (Event Object)，裡面包含了所有與這個事件有關的屬性，並且以「參數」的形式傳給我們的 Event Handler：
```JavaScript
var btn = document.getElementById('btn');

// 參數 e 就是上面說的事件物件 (Event Object)
// 因為是參數，當然也可以自己定義名稱
btn.addEventListener('click', function(e){ console.log(e); }, false);
```

### Event.preventDefault()
prevent default 防止預設行為觸發，它指的是瀏覽器的預設行為，並非事件傳遞。
比如最常見的 `<a>` 標籤 href 跳轉，或 `<form>` 的 submit action 等。
```JavaScript
form.addEventListener('submit',e=>{  
e.preventDefault();  
// 把原生的 Form submit 跳轉行為停掉  
})
```
但要注意的是， `event.preventDefault()` 並不會阻止事件向上傳遞 (事件冒泡) 。
另外，值得一提的是，在 event handler function 的**最後**加上 `return false;` 也會有 `event.preventDefault()` 的效果，但切記<u>切記不可以加在前面</u>，若是加在前面 event handler function 就直接結束了。

### 阻擋事件冒泡傳遞 event.stopPropagation()
如果我們想要阻擋事件向上冒泡傳遞，那麼就可以利用 event object 提供的另一個方法： `event.stopPropagation()`。
>[重新認識 JavaScript: Day 15 隱藏在 "事件" 之中的秘密](https://ithelp.ithome.com.tw/articles/10192015)

