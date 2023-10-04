#front-end #JavaScript 
String 是基本型別
為什麼 string 有 methods 可以用？
當 call a method 的時候，JS 會自動把字串轉換成==string object==

在拿到字串後，通常會統一先轉成小寫 `toLowerCase`，會比較好處理。

- indexOf / lastIndexOf
- slice
- toLowerCase / toUpperCase
- trim
- replace
- includes
- startsWith / endsWith
- split
- join
- padStart / padEnd
- repeat
- concat *(補充)*

---

1. `slice()`
先來看看 MDN 上面的解釋：
   > The `slice()` method of String values extracts a section of this string and returns it as a new string, without modifying the original string.

由此可知，slice 代表的是複製，複製開始與結束點（結束點不算）中的內容，可作用於 String 和 Array 上。
用法：  
begin 為開始的索引值，負數代表從後面開始算起，-1 為倒數第一個元素。  
end 為結束的索引值，沒有填寫時則得到 arr 中的所有元素。
因為是做 **shallow copy**，所以原值不改變。
```javascript
var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
var fruit1 = fruits.slice(1);
var fruit2 = fruits.slice(1, 3);
var fruit3 = fruits.slice(-3);

// fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
// fruit1 contains ['Orange', 'Lemon', 'Apple', 'Mango']
// fruit2 contains ['Orange', 'Lemon']
// fruit3 contains ["Lemon", "Apple", "Mango"]
```

2. `split()`

> The `split()` method of **String** values takes a pattern and **divides** this string into an ordered list of substrings by searching for the pattern, puts these substrings into an array, and returns the array.

從指定的地方開始分割字串，==會回傳一個陣列==，並以逗號隔開每個元素，也可以限制返回值的最大長度。
如果將 limit 參數設定為零，則會返回空陣列 []。
```
split(separator)
split(separator, limit)
```

```JS
const str = 'The quick brown fox jumps over the lazy dog.';

const words = str.split(' ');
console.log(words[3]);
// Expected output: "fox"

const words2 = str.split(' ', 3);
console.log(words2);
// Expected output: Array ["The", "quick", "brown"]

```

padding method
add a number of character to the string, until the string has a certain desired length
