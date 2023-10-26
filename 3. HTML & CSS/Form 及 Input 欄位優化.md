# Textarea
想要改變畫面中 textarea 的高度，可以在 HTML 中添加 `row` 屬性將文字區域展開到指定的行高，但這麼做有一個問題：我們沒辦法去預判使用者想要輸入幾行、想要輸入多少個字。

解決方法：
1. form-sizing: normal
2. height: max-content

`<textarea wrap="">`：分成 soft 跟 hard 兩種。
