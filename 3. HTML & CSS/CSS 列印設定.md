#CSS 

### 設定 `@media print`
media 最常被使用在製作 RWD 切版時，用 screen 辨別裝置大小，但它其實還可以辨別列印狀態。我們可以設置 `@media print`，告知瀏覽器你想要的列印設定。

### 列印背景色
`print-color-adjust` 這個屬性用以設定瀏覽器列印背景顏色時的行爲，此屬性有兩個比較重要的參數：
- economy（默認值）：允許瀏覽器自動調整
- exact：使用你設定好的樣式顏色

### 換頁設定
- break-after
- break-before
- break-inside
這三個屬性可以**設定元素跟分頁斷點之間的關係**，可以利用這些屬性達成強迫元素前後換頁等效果，詳細內容可以看 MDN 說明。在此次的範例中，我們需要第三個屬性，元素內容中間，不能被換頁。

### 設定 `@page`
利用 `@page` 可以設定紙張配置。有兩個比較常用的屬性：
- size：指定目標紙張寬高度或是通用尺寸（A4、A5），以及頁面方向（portrait / landscape）。
- margin：利用 margin 設定邊距，亦可以利用 css 選擇器，選擇第一頁。


