#front-end #JavaScript 
# 基本
## push()
`push()` 可以將某些值加入到陣列的**最後**一個位置，不限制添加數量，欲添加的內容使用逗號隔開即可，加入後陣列長度會增加。
使用`push()` 後會改變原本的陣列內容。

## pop()
`pop()` 會移除（取出）陣列的**最後**一個元素。
使用`pop()` 後會改變原本的陣列內容。

## unshift()
`unshift()` 會將指定的元素添加到**第一個**位置。
使用`nushift()` 後會改變原本的陣列內容。

## shift()
`shift()`會移除（取出）陣列的**第一個**元素。
使用`shift()`後會改變原本的陣列內容。

## splice()
`splice()` 可以移除或新增陣列的元素，它包含了三個參數。
第一個是要移除或要添加的序列號碼（必填），第二個是要移除的長度（選填，若不填則第一個號碼位置後方的所有元素都會被移除，若設定為 0 則不會有元素被移除），第三個是要添加的內容（選填）。
會改變原陣列的內容。
```javascript
let a = [1, 2, 3, 4, 5, 6, 7, 8;
a.splice(5, 1);

console.log(a);
// [1, 2, 3, 4, 5, 7, 8]
```


# 進階
## Array.filter()
`filter()` 依照字面上的意思，可以幫助「**過濾**」元素，會將陣列中的「每一個」元素帶入指定的函式內做判斷，如果元素符合判斷條件則會傳出，成為一個新的陣列元素，可以幫忙找出**所有**符合條件的元素。
例如你有一串數字，但只想要留下大於 100 的數字，就可以這樣子寫：
```javascript
const nums = [89, 32, 104, 46, 249, 71, 515];

const numsBiggerThan100 = nums.filter(num => num > 100);

console.log(numsBiggerThan100);
// [104, 249, 515]
```

## Array.reduce()
`reduce()` 方法將一個累加器及陣列中每項元素（由左至右）傳入回呼函式，將陣列化為單一值。簡單來說，會將「上一次的結果」放進「這一次的參數」執行。
介紹到 `Array.reduce` 的用法幾乎都是用在計算加總（包括 [MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)也是），像是這樣子：
```javascript
const nums = [89, 32, 104, 46, 249, 71, 515];

const total = nums.reduce((prevTotal, num) => prevValue + num, 0);

console.log(total);
// 1106
```
可以看到上方的 `Array.reduce` 接收的方法有兩個參數，一個是 `prevTotal`，另一個是 `num`，`prevTotal` 的值會是上一次的回傳值，而 `num` 就是當前的數字。
比較特別的是 `Array.reduce` 在第一次執行的時候，會沒有上一次的執行結果，所以 `Array.reduce` 可以有第二個參數指定初始值（上方程式碼區塊第三行的 0），但如果沒有特別指定的話預設值也會是 0。

## Array.find()、Array.findIndex()
`find()`會將陣列中的「每一個」元素帶入指定的函式內做判斷，並會回傳**第一個**符合判斷條件的元素，如果沒有元素符合則會回傳 undefined。
`findIndex()`會將陣列中的「每一個」元素帶入指定的函式內做判斷，並會回傳第一個符合判斷條件元素的位置號碼，如果沒有元素符合則會回傳 **-1**。
```javascript
const todos = [
  { id: 1, title: '倒垃圾' },
  { id: 2, title: '洗衣服' },
  { id: 3, title: '運動' },
];

const targetTodo = todos.find(todo => todo.id === 2);
console.log(targetTodo);
// { id: 2, title: '洗衣服' }

const targetTodoIndex = todos.findIndex(todo => todo.id === 2);
console.log(targetTodoIndex);
// 1
```

## Array.map()
`map()` 方法會建立一個新的陣列，它會將 array 中**所有的值都經過處理**，且新陣列的內容為原陣列的每一個元素經由回呼函式運算後所回傳的結果之集合。
```javascript
const todos = [
  { id: 1, title: '倒垃圾' },
  { id: 2, title: '洗衣服' },
  { id: 3, title: '運動' },
];

const todoIds = todos.map(todo => todo.id);
console.log(todoIds);
// [1, 2, 3]

const todoStringIds = todos.map(todo => String(todo.id));
console.log(todoStringIds);
// ['1', '2', '3']
```
> 如果有在寫 React 的話，因為 React 沒有像 Vue 一樣的 `v-for` 語法糖，因此在需要顯示某個 array 的資料時，幾乎都會使用 `map` 處理。

另外，因為 `map` 方法會產生一個新陣列，如果不想建立新的陣列，就可以採用 `forEach` 方法。

## Array.forEach()
`forEach()`會將陣列中每個元素套用到指定的函式裡進行運算，函式有三個參數，第一個參數表示每個元素的值 ( 必填 )，第二個參數為該元素的索引值 ( 選填 )，第三個參數則表示原本的陣列 ( 選填 )。
```javascript
let arr = [1, 2, 3, 4, 5];

arr.forEach((item, index, arr) => { arr[index] = item * 10; });

console.log(a);
// [10, 20, 30, 40, 50]
```

## Array.includes()
`Array.includes` 會接收一個值，然後判斷該值有沒有在 array 中，有的話就回傳 true，否則回傳 false。使用方法如下：
```javascript
const nums = [1, 2, 3, 4, 5];

const result = nums.includes(3);

console.log(result)
// true
```
但是 `Array.includes` 有個小缺點，就是如果要比對的 array 裡面是 object 的話，就不能用 `Array.includes` 去判斷（可能要搭配 `Array.map` 先把 id 取出來）。

## Array.some()
`Array.some` 是指在執行過程有一個 true 就會回傳 true。它可以用來當作 `includes` 方法的高階版，判斷某個符合條件的 object 是否有存在在 array 中：
```javascript
const todos = [
  { id: 1, title: '倒垃圾' },
  { id: 2, title: '洗衣服' },
  { id: 3, title: '運動' },
];

const result = todos.some(todo => todo.id === 2);

console.log(result);
// true
```

## Array.every()
`Array.every` 則是要執行過程全部都是 true 才會回傳 true，否則就是 false，在實務上可以在表單驗證時使用，代表當所有的驗證都回傳 true 才算通過。
以下是一個判斷 input 是否為有效數字的簡單例子：
```javascript
const validations = [
  num => Number.isInteger(num),
  num => !Number.isNaN(num),
  num => num > 100,
  num => num < 1000,
];

const price1 = 210;
const isValid1 = validations.every(validation => validation(price1));
console.log(isValid1);
// true

const price2 = '210';
const isValid2 = validations.every(validation => validation(price2));
console.log(isValid2);
// false
```

---

Reference：
>[JavaScript Array 陣列操作方法大全 ( 含 ES6 )](https://www.oxxostudio.tw/articles/201908/js-array.html#array_every)

