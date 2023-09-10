身份驗證功能。
最簡易的身份驗證功能，是使用者在客戶端透過基本的帳號與密碼向後端伺服器驗證身份。伺服器會經過一連串的驗證流程，驗證成功後透過如 Session / Cookie 機制，在客戶端保存用戶登入的狀態資訊。
![[user-valiation.png]]
**缺點：安全性與維護**
必須自己維護驗證的機制與穩定性，也必須隨時檢視使用的驗證和保存機制，是否符合當前普遍認為的安全性等。例如將密碼進行雜湊後再儲存與比對即是一個普遍的做法。

# OAuth 2.0 解決方案
我們在許多拜訪的網站想要登入時，時常能看到像下圖 Medium 登入跳窗，提供多種登入的方式。在不經意的點擊下，我們其實已經使用到 OAuth 的流程。
>OAuth 是一個開發標準（[Open Standard](https://en.wikipedia.org/wiki/Open_standard)）用來處理有關「授權」（Authorization）相關的行為。

![[medium-sign-in-popup.png]]

這個使用 OAuth 的流程白話來說：「我們允許並授權當前的應用程式（在這是指 Medium）有限度的取得我們在 Facebook、Google 或其他平台的相關資訊」——**使用者身份驗證的工作基本上是委由選擇的平台完成**，當驗證成功，且用戶同意，應用程式才得以前往取得所需要的資源。

常見角色與詞彙：
- Resource Owner
  授權 Client 去取得 Resource Server 裡面存放的 Protected Resource，也就是**使用者本身** (end-user)，也稱終端使用者。
- Resource Server
  存放 Protected Resource 的伺服器，可以接受來自 Client 透過 Access Token 發出的請求。
- Client
  代表 Resource Owner 去存取 Protected Resource 的應用程式，就是 To-do list 作業本人。
- Authorization Server
  認證過 Resource Owner 並且 Resource Owner 許可之後，核發 Access Token 的伺服器。
- Access Token
  Access Token 是 Authorization Server 簽發的。應用程式最終能拿著這個 Token 向 Resource Server 取得需要的資源。

## OAuth2.0 四種授權類型流程
### Authorization Code 授權碼
這是最常見的類型，Server-side Application （Web server applications）最為適用——通常會由後端伺服器負責產生頁面（View）回傳給前端渲染。如此一來，大部分的邏輯處理程式碼，以及像應用程式的 Client Secret 等重要機密資訊，都能在伺服器端被保存，而非完全公開。
### Implicit Token 驗證
適合 Client-side applications 的類型——**通常會是整個應用程式都在前端運行**，依需求向後端 API 取得資料。例如單純的靜態網站或 Single Page Application(SPA) 都適用。

由於整個應用程式都在前端運行，所以會**缺少「後端伺服器透過 Authorization Code Grant 交換 Access Token 」的步驟**。取而代之的是請 Authorization Server 直接核發 Access Token。
特別留意：不像 Authorization Code Flow，這邊是由前端獲得與管理 Access Token，並帶著 Access Token 發出請求前往取得資源，因此在安全性上「相對脆弱」。

### Resource Owner Password Credentials
此流程是由使用者提供帳號與密碼等資訊給應用程式，由應用程式直接向 Authorization Server 交換 Access Token，體驗上和以往的帳號密碼登入雷同。

帳號與密碼等機密資訊（credentials）可能會被應用程式儲存起來，作為往後交換 Access Token 使用。因此「必須是使用者高度信賴的應用程式」才適合使用，且唯有前兩種皆不可行時，才會考慮使用當前類型的流程。因此，適用的情境，可能像公司內部的系統。

### Client Credentials
適合用在 machine-to-machine (M2M) applications——通常是由應用程式向 Authourization Server 請求取得 Access Token 以獲取「自己」的相關資源，而非使用者的資源。

這個流程已經跳脫使用者，因此，使用者身份驗證的流程將不再需要。取而代之的，是應用程式必須向 Authorization Server 提供驗證所需的自身資訊。
