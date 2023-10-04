## 專案結構
概念上：
- node_modules
- public -> 放置公開檔案（可透過瀏覽器被下載）如圖片等
- src
  - pages -> 網站主要頁面，副檔名為 `.astro`，寫法類似 HTML
    - blog -> 部落格文章放置處
  - style -> 網站 CSS 樣式、JavaScript 等
  - components -> 元件
  - scripts -> JS 檔案，大多用來操控使用者互動效果
  - layouts -> 用來設計排版、網頁布局
- package.json

## Blog Posts 頁面
在畫面上渲染出每一則 blog posts：使用 `Astro.glob()` 會回傳一個陣列的物件。

## Tag 頁面
在 `pages` 資料夾底下創建一個 `tags` 的資料夾，裡面新增一個 `[tags].astro` 的檔案，用來存放及管理所有部落格文章會用到的 tag。

確保每一篇文章都至少含有一個 tag，且 tag 名稱須以陣列的形式儲存，例如 `tags: ["blogging"]`。

