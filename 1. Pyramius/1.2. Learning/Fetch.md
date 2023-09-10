`fetch()` 是一個全域的方法，包含了需要 fetch 的網址和對應的屬性設定 ( 例如 method、headers、mode、body...等，最基本的寫法屬性不一定要填 )，執行之後會送出 Request，如果得到回應就會**回傳帶有 Response 的 Promise 物件**，使用 then 將回傳值傳遞下去。
```JavaScript
fetch('網址')
.then(function(response) {
    // 處理 response
}).catch(function(err) {
    // 錯誤處理
});
```



>[JavaScript Fetch API 使用教學](https://www.oxxostudio.tw/articles/201908/js-fetch.html)
>[WebAPIs Fetch API - PJCHENder](https://pjchender.dev/webapis/webapis-fetch/)
### 補充 - HTTP Status Code
HTTP Status Code，又叫做「HTTP 狀態碼」，是伺服器對於瀏覽器的請求所給出的回應。當你瀏覽一個網站的時候，你的瀏覽器會向網站伺服器發送請求（request），每個請求伺服器都會用一個三位數的代碼來回應瀏覽器的請求，這就是 HTTP Status Code。

- 200 OK
  請求成功。成功的意義依照 HTTP 方法而定： GET：資源成功獲取並於訊息主體中發送。 HEAD：entity 標頭已於訊息主體中。 POST：已傳送訊息主體中的 resource describing the result of the action。 TRACE：伺服器已接收到訊息主體內含的請求訊息。
- 201 Created
  請求成功且新的資源成功被創建，通常用於 POST 或一些 PUT 請求後的回應。
- 400 Bad Request
  此回應意味伺服器因為收到無效語法，而無法理解請求。
- 401 Unauthorized
  需要授權以回應請求。它有點像 403，但這裡的授權，是有可能辦到的。
- 403 Forbidden
  用戶端並無訪問權限，例如未被授權，所以伺服器拒絕給予應有的回應。不同於 401，**伺服端知道用戶端的身份**。
- 404 Not Found
  伺服器找不到請求的資源。因為在網路上它很常出現，這回應碼也許最為人所悉。