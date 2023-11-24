# rem()
在 JavaScript 中，我們可以使用 `%` 來取得兩數相除的餘數。
``` javascript
console.log(9 % 4); // 1
console.log(5 % 4.1); // 0.9
console.log(1003 % 5); // 3
```

而在 CSS 中，則可以利用 `rem()` 函式來取得餘數。
``` css
line-height: rem(9, 4); /* 1 */
line-height: rem(5, 4.1); /* 0.9 */
line-height: rem(1003 % 5); /* 3 */
```

有時候我們也必須將單位考慮進去：
``` css
rotate: round(20deg, 5deg); /* 0deg */
rotate: round(20deg, 7deg); /* 6deg */
rotate: round(20deg, 3deg); /* 2deg */
```

# mod()
