#front-end #JavaScript 
# Promise
Promise 本身是用來改善 JavaScript **非同步**的語法結構。
Promise 的三種狀態：
- Pending：尚未得到結果
- Resolved：事件已經執行完畢且成功操作，回傳 `resolve` 的結果
- Rejected：事件已經執行完畢但操作失敗，回傳 `rejected` 的結果
上列的三種狀態每次執行必定會經過 Pending，接下來進入 Fulfilled 或 Rejected 的其中之一，並且可以使用 `then()` 及 `catch()` 取得成功或失敗的結果。

# Async / Await
