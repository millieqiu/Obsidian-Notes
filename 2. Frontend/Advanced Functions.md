#front-end #JavaScript 
# Default Parameters 預設參數

在 ES5 的時代，我們可以透過短路求值來幫函式設定預設值：
```js
const link = function (point, url) {
    let point = point || 10
    let url = url || 'http://google.com'
    ...
}
```

但在 ES6，發展出了一種新的替函式參數設定預設值的方法：
```js
const link = function (point = 10, url = 'http://google.com') {
    //...
}
```

預設參數也可以設成別的變數，例如：
```js
function foo(a = 0, b = a + 100) {
  console.log(a+b)
}

foo() // 100
foo(1)  // 102
foo(1, 2) // 3
```

參數宣告的順序固定，是不能任意跳過的。
如果已經有給預設參數，且真的需要跳過其中一個變數，可以在呼叫函式時將之設成 `undefined`，因為把參數設成 `undefined` 就等於沒有給變數。

# Arguments - Value vs. Reference
在理解 arguments之前，得先理解何謂參數，參數為要帶入函式中的變數，也就是我們在執行函式時可以任意帶入的值，下面例子中，fruit 及 vegetable 就是所謂的參數。
```js
function eatFood(fruit, vegetable) {
  console.log(fruit)
  console.log(vegetable)
}
```

## 什麼是 arguments
arguments 是一個對應傳入函式之引數的類陣列（Array-like）物件。簡單來說也就是 parameters 的集合的概念。以上面的例子來說，arguments 就是包含了 fruit 跟 vegetable 的一個**類陣列物件**。

它是類陣列，不是真的陣列，雖然可以用 `arguments.length` 來取得裡面參數的數量，也可以直接使用 `arguments[index]` 來取得或修改特定位置的參數，但它並不能使用陣列的操作方法。

## JS 是「傳值」還是「傳址」？

>[重新認識 JavaScript: Day 05 JavaScript 是「傳值」或「傳址」？](https://ithelp.ithome.com.tw/articles/10191057)
>[深入探討 JavaScript 中的參數傳遞：call by value 還是 reference？](https://blog.techbridge.cc/2018/06/23/javascript-call-by-value-or-reference/)


# First-class & Higher order functions

Firtst class functions
- JS 將函式視為「一等公民」
- 這意味著在 JS 的世界裡，函式跟 values 是相同的概念
- 函式是另一種物件的資料型態
因此我們可以：
1. 將函式儲存在變數或者屬性裡：利用函式表達式宣告，或將函式宣告成物件的方法（Method）。
2. 將函式當作其他函式的 arguments 傳入：
```js
const greet = () => console.log('Hello!');
btn.addEventListener('click', greet);
```
3. 從其他函式中回傳（return）另一個函式。
4. 不只 array 跟 object 有方法，**函式也有自己的方法**。例如 `bind`。

## Higher-order function 的定義
A function that **receives** another functions as an argument, that **returns** a new function, or both.
![[udemy.png]]

## Callback function
看自己的文章：
>[Daily notes #2：什麼是 Callback function？](https://millieee-blog.coderbridge.io/2023/08/31/what-is-callback-function/)


## Functions returning functions


# Call, Apply and Bind methods
## 前情提要：What's THIS?
- `this` 是 JavaScript 的一個關鍵字。
- `this` 是 function 執行時，自動生成的一個內部物件。
- 隨著 function 執行場合的不同，`this` 所指向的值，也會有所不同。
- 在大多數的情況下， `this` 代表的就是呼叫 function 的物件 (Owner Object of the function)。

`this` 代表的是 **function 執行時所屬的物件，而不是 function 本身**。
**在 eventhandler function 中，`this` 關鍵字會指向偵聽器綁定的元素上。**

## Call
```
fun.call(thisArg[, arg1[, arg2[, ...]]])
```
參數：
**`thisArg`**：呼叫 `fun` 時提供的 `this` 值。
**`arg1, arg2`**：原始函式的其他參數。

## Apply
apply 方法的參數為 `thisArg` 以及一組陣列資料，並且回傳的會是一個「陣列」。
現在這個方法在 Modern JS 中已經不常被使用，取而代之的會使用 call + spread operator。

## Bind
重要！
會回傳一個新的函式，幫助定義新的 this 範圍。

