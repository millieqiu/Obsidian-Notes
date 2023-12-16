#front-end #JavaScript 
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
