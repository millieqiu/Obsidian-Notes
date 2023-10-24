# NPM
npm 即為 Node Package Manager 的縮寫，開發者可以透過 Node 隨附的 [npm cli](https://github.com/npm/cli)，進行套件的安裝及管理。
在程式開發的領域中，有許多 JavaScript 工具，像是 jQuery, Express, Vue, React 等。**為了把這些工具都統整在一個地方，讓開發者方便搜尋和使用，於是就有了 Node 套件管理器**。
例如在專案資料夾的終端機中輸入 `npm install express` ，npm 便會自動尋找 express  框架，取得最新版本，下載到專案中的 node_modules 資料夾中。

npm 安裝指令：
```
npm install Vue@^2.6.14
            ^^^^ ^^^^^^
            套件名稱 版本
```

# Webpack
是一個「打包工具」，將眾多模組與資源打包成一包檔案，並**編譯**我們需要預先處理的內容，變成瀏覽器看得懂的東西，讓我們可以上傳到伺服器。
### 為什麼需要模組化設計？
剛學 JavaScript 時，會將程式碼直接放在 HTML 的 script 標籤裡。
但隨著功能越來越多我們會把 `script` 裡面的內容獨立出來到一個 JS 檔中：
```html
// index.html

<script src="./main.js"></script>
```

當開發人員越來越多，功能也一直再新增，如果都繼續編寫同一個 JS 檔，當行數不再是 24 而是 1000，將變得非常難以閱讀及維護。為了避免這樣的情況發生，我們可以拆成多個 JS 檔：
```html
// index.html

<script src="./utils.js"></script>
<script src="./main.js"></script>
```
然而，雖然目前我們雖然把程式碼分開了，但實際上它還是在同一個作用域下，其中的變數是會互相影響。
### ES6 Module
ES6 出來之後，終於有了正式的模組化規範，如下：
```JavaScript
// utils.js

let author = 'Mr.A'

// 需要先寫export，此檔案未來才有辦法被其他檔案import
export function getAuthor(){
    return author
}
```

```JavaScript
// utils2.js

// import剛才的utils.js
import { getAuthor } from './utils.js'

let author = 'Mr.B'
let authorFromUtils = getAuthor()

export function getTwoAuthors(){
    return author + '_&_' + authorFromUtils
}
```

```JavaScript
//main.js
import { getAuthor, author } from './utils.js'
import { getTwoAuthors } from './utils2.js'

console.log(getAuthor()) // 'Mr.A'
console.log(getTwoAuthors()) // 'Mr.B_&_Mr.A'
```

當用 npm 安裝套件後，會放到 node_modules 這個資料夾裡，這樣子我們引入的路徑就可能要改寫成 `'./node_modules/xxx/index.js'` 這樣子。
假設哪天套件的入口點換了，整個專案有使用到這個套件的都需要改寫，這樣其實很不方便。除此之外，有些套件輸出是寫 `module.exports`，我們也沒辦法使用 `import` 來引入，因此這個時候，我們就需要藉由 Webpack 的幫助。

✏ export 分兩種：
- 具名：每個要 export 的東西都有命名，載入時要用 {}
  但如果載入時想改名也可以 { 原名 as 新名}
- 匿名：export default > 一個檔案只能有一個

### 認識 Webpack
1. **`mode`** 這個屬性不寫的話預設會是 `production`，代表在生產環境下使用，所以會自動幫你壓縮以及優化。`development` 這個模式代表開發的時候，打包的速度較快。
2. 打包（Bundle）多個 `.js` 檔案成單一檔案。
   你可以寫模組化的 JavaScript，你不再需要在 HTML 中引入每個 JavaScript 檔案（`<script src="..."></script>`），如果有眾多的 `.js` 檔案，可以透過 Webpack 來設定。

#### 設定
- 在專案根目錄建立 `webpack.config.js`。
```JavaScript
// webpack.comfig.js
const path = require("path"); // 引入 path 來解決巢狀引入路徑問題

module.exports = {
  mode: "development", // 設定開發模式就不會 minify
  devtool: "none", // 編譯後的程式碼不會有 eval 這樣的用法
  entry: "./src/index.js",
  output: {
    filename: "hello.js", // 編譯後的檔名
    path: path.resolve(__dirname, "your-directory-name") // 編譯後要放在哪個資料夾
  }
};
```
Webpack 只能讀懂 JavaScript 的檔案，因此入口與出口都需要是 .js，如果想打包 CSS 檔案，則需要安裝其他套件，例如 css-loader 或 sass-loader 等。

1. Entry：告訴 webpack 要使用的進入點是哪隻檔案，預設會使用 `./src/index.js`。
2. Output：要把 bundle 過的檔案放在哪裡及其檔名，預設會使用 `/dist/main.js`。
3. Loaders（modules）：雖然 webpack 本來就可以了解 JavaScript 和 JSON 檔，但實際的應用程式中仍包含許多其他類型的檔案（例如，圖檔），這時候會需要透過 loader 來處理 JS / JSON 以外的檔案類型。在設定時，是透過 `module.rules` 的屬性來設定。
4. Plugins：
   ✏由於你可以根據需求在設定檔的不同位置重複使用該 plugin，因此在使用 plugin 是需使用 `new` 來確保每個 plugin 是獨立的 instance。
5. Mode：預設是 production，也可以是 development 或 none。

==MiniCssExtractPlugin==：將 stylesheet 拆成獨立的 CSS 檔。
ℹ備註：Webpack 4 以前使使用 extract-text-webpack-plugin；Webpack 4 之後則是使用 mini-css-extract-plugin。

#### Development (開發環境) 與 Production (生產環境)
- Source map：透過 source map 可以在程式碼出錯時，方便我們找到錯誤的程式碼在哪一隻檔案。
```JavaScript
// webpack.config.js

module.exports = {
	devtool: 'inline-source-map'
	// 以下省略
}
```
- 使用觀察模式（Using Watch Mode）
  透過 `watch` 指令可以讓 webpack 監控所有依賴圖（dependency graph）下的檔案有無變更，如果其中有檔案變更了，程式碼就會被重新編譯，因此不需要手動執行 build 指令。缺點是，為了看到修改後的實際效果，**你需要刷新瀏覽器**。

### 打包的用意
1. 必要的編譯語法：例如瀏覽器不認識 `.vue` 檔，需要編譯成瀏覽器能讀懂的 `.js` 檔和 `.css` 檔。
2. 壓縮成一個或較少份檔案，可以減少 HTTP Requests 的次數。
3. 「將程式碼變短」（Minify），節省瀏覽器解析的時間：在不影響程式運作的前提下，去除不必要的空白字元、註解，將變數名稱、函數名稱、參數名稱縮短等。
4. 「將程式碼變醜」（Uglify），讓赤裸的前端不要那麼赤裸，比較不方便被外人研究。
5. 處理第三方套件模組的引入跟編譯：開發團隊會透過 npm 或 yarn 安裝專案所需的第三方套件。  
套件模組都放在 node_modules 內，卻可以透過 `import from "xxx"` 直接使用，不需要寫出該模組的完整路徑，這是打包工具的功勞。

