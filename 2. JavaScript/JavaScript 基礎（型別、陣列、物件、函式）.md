#front-end #JavaScript 
# 基本型別
基本型別有number、string、boolean、null、undefined、symbol，而物件型別就是物件與其子型別（subtype），例如：物件、陣列、函式、日期等。

## 物件 (Object)
函式也可以是物件的成員。
物件的成員分成兩種：屬性(非函式)及方法(函式)，因此常聽到「物件的方法」就是指「物件內的函式」，而==在物件方法中使用 this 則會指向物件本身==。

物件表示法：
```JavaScript
let obj = {
	x: 1,
	y: 2,
	show: function() {
		console.log('Hello World');
	}
}
```

建構式：
```JavaScript
let obj = new Object();
obj.x = 1;
obj.y = 2;
obj.show = function() {
	console.log('Hello World');
};
```

物件取值的方式有兩種，用**點語法**或是**中括號**：
```javascript
var obj = {
  myName: 'Ray',
  num: 1,
  family: {
    mon: '漂亮阿姨',
  },
  objFn: function() {
    console.log('漂亮阿姨回家囉');
  },
}
```
透過點運算子假使我們要取得 `myName` 只需要寫 `obj.myName` 即可。
而中括號取值方式則是 `obj['myName']` 中括號取值裡面是使用字串的方式去取值，使用中括號取值的方式還有另一個好處，可以傳入變數來取值。


## 陣列 (Array)
JavaScript 內建物件的一種，是可依照**順序**存放資料的容器，利用有順序的編號來管理內部資料。

# DOM Tree
HTML 文件中的各個標籤(文字、圖片)都定義成物件，並用節點 Node 來稱呼。節點共有四個種類：
- Document ，也就是 HTML 的開端
- 各種標籤如`<div>`被我們稱呼為 Element
- 被標籤包起來的字，如 `<h1>Hello</h1>` 的 Hello 是 Text
- HTML 屬性，如 `<img src>` 的 src 則被稱呼為 Attribute

DOM Method 不屬於 JavaScript 的語法，而是 Web API 的一種，可以和 JS 互動。除了 DOM 以外還有很多 Web API 例如 Timer (計時)、Fetch API......等。

document.querySelector 只會選取第一個符合的元素，如果要選取多個符合的元素，那麼你就必須要使用 document.querySelectorAll，但是要注意 document.querySelectorAll 會回傳一個 NodeList，所以你必須要使用 **forEach** 或是 **for 迴圈**來選取。

==`document.querySelector` 在選取上是比較方便且彈性的，但如果以效能來講，`document.getElementById` 的效能會比較好。==
> `document.querySelector` 大多在選取時，大多都是採用 CSS 的選取方式，因此 `document.querySelector` 會需要先解析 CSS 的選取方式，然後再去選取元素，而 `document.getElementById` 則是直接依照 ID 選取元素，所以在效能上就會比較好。

###### 🐱 讀書會補充
- `window` 跟 `document` 的差別
- window 的 `innerHeight` 跟 `outerHeight`
- document 的 `clientHeight`、`offsetHeight`、`scrollHeight`

- `textContent`：
- `innerHTML`：早期動態產生內容時都是使用這個，但風險是容易遭到「跨網站指令碼攻擊（XSS）」。
>[零基礎資安系列（二）-認識 XSS（Cross-Site Scripting）](https://tech-blog.cymetrics.io/posts/jo/zerobased-cross-site-scripting/)

# Function 函式
「函式」指的是將一或多段程式指令包裝起來，可以重複使用並方便維護。

宣告函式的方法有好幾種，但不管是什麼方式，通常一個函式會包含三個部分：
- 函式的名稱（也可能沒有名稱，稍後會提到）
- 在括號 `( )` 中的部分，稱為「參數（arguments）」，參數與參數之間會用逗號 `,` 隔開
- 在大括號 `{ }` 內的部分，內含需要**重複執行的內容**，是函式功能的主要區塊。

**基本結構：**
-  parameter
  指會帶入函式的變數名稱。
-  argument
  實際帶入函式的「值」。
![[ExportedContentImage_00.png]]
### 回傳值（return value）
所有的函式都有回傳值，回傳值可以用關鍵字 `return` 來指定：
```javascript
function greeting(name) {
	return `hi, ${name}` // 這是回傳值
}

greeting('Anne');
```
如果沒有特別指定，回傳值一律會是 `undefined`。

## 函式運算式（Function Declaration）
- 具名函式
```javascript
function square(number) {
	return number * number;
}
```

## 函式表達式（Function Expression）
- 匿名函式
```javascript
const square = function (number) {
	return number * number;
};
```

> [!note] 
> 
還有另一種方式就是透過 `new Function` 關鍵字建立函式，直接使用 `Function`（注意 F 大寫）這個關鍵字來建立函式物件。 使用時將參數與函式的內容依序傳入 `Function`，就可以建立一個函式物件了。 像這樣：

```javascript
// 透過 new 來建立 Function
var square = new Function('number', 'return number * number');
```
透過 `new Function` 所建立的函式物件，運作效能較差，所以通常實務上也較少會這樣做。

### 函式作用域
Function 擁有自己的作用域，可以在函數內定義的任何變數（local variable），且只有在函數裡面才可以存取到這個變數。
在函數裡面除了可以存取到局部變數（local variable），也可以存取到全域變數（global variable）。
```javascript
// 全域變數 - global scope
var num1 = 20;
var num2 = 3;
var name = 'Mike';

// 這個函數定義全域空間 - global scope
function multiply() {
    // 函數內部可以存取到全域變數
    return num1 * num2;
}

// 輸出 60
console.log(multiply());

function getScore () {
    // 局部變數 - function scope
    // 作用範圍只在函數內部
    var num1 = 2;
    var num3 = 4;
    
    // 如果沒加 var 宣告變數，這個變數則是一個全域變數
    num2 = 5; // 存取到全域變數 num2
    num4 = 6; // 宣告一個新的全域變數 num4

    // 函數也可以宣告在其他函數內部 (nested function) - function scope
    function add() {
        // 內部函數可以存取到外部函數的局部變數
        return name + ' scored ' + (num1 + num2 + num3);
    }
  
    return add();
}

console.log(getScore()); //  "Mike scored 11"

// 會存取到全域變數 num1，輸出 20
console.log(num1);

// 會存取到全域變數 num2，輸出 5
// 因為全域變數 num2 在函數內部被設成 5
console.log(num2);

//會存取到全域變數 num4，輸出 6
console.log(num4);

// 全域空間存取不到 function 內部的變數
// 會發生錯誤 - Uncaught ReferenceError
console.log(num3);

// 全域空間也存取不到 function 的內部函數
// 會發生錯誤 - Uncaught ReferenceError
console.log(add());
```
###### 🐱 讀書會補充
用匿名是函式是因為它只會用到一次，詳情：
使用匿名函式的時機 -> 如果某個函式裡執行的很複雜，不想影響到外部。
var a = function () ...
`a` 的作用域在哪，function 的範圍就在哪。
https://hackmd.io/@pikachuchu/rk7a2uLTd

- `return` 後函式就會中斷執行。
- 如果有很多個 if 判斷，可以用 return 中斷，以免最前面就出錯（判斷出 false）了，還一定要執行完全不的函式。

>[重新認識 JavaScript: Day 10 函式 Functions 的基本概念](https://ithelp.ithome.com.tw/articles/10191549)
## Arrow Function 箭頭函式
### Arrow Functions 小檔案
---
- ECMAScript 2015 (ES6) 導入的新特性。
- 稱為 Arrow Function Expression，或稱 Fat Arrow Functions，最初在 CoffeeScript 的語法中流行。
- 在函數定義的語法上更為簡潔。
- 函數運作行為上和傳統語法所定義的函數有差異，例如 `arguments`、`this`。

### Arrow Functions 使用的注意事項
---
1. ==沒有 Hoisting 效果==
Arrow Functions 是表達式的語法形式，就像函式表達式 (Function Expression) 那樣，函數定義的部分不會被 Hoist。換言之，**定義必須寫在使用之前**。
```JavaScript
console.log( sayHello );    //undefined
console.log( sayHello() );  // TypeError: sayHello is not a function
var sayHello = () => `Hello OneJar!`;
```
2. 建議使用 `const` 做名稱部分的宣告
3. 不會產生新的 `arguments` 物
4. `this` 運作行為的不同
前面介紹 `this` 時，提到判斷 `this` 代表什麼物件的大原則：**看呼叫時的物件是誰**；Arrow Functions 的 `this` 和傳統函數的一個重大差異就是看的是**語彙位置**。
傳統函數每次呼叫函數，都會建立一個新的函數執行環境 (Function Execution Context)，然後建立一個新的 `this` 引用物件，指向當下的呼叫者。
而 Arrow Functions 則不會有自己的 `this` 引用物件，呼叫 `this` 時，會沿用語彙環境外圍的 `this`。