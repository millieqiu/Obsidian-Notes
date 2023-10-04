#front-end #JavaScript 
ES6 發展出的新資料型態，儘管\在其他程式語言中已經是非常普遍也很常見的資料型態，但 JS 在 ES6 過後才正式推出。
ES6 中如果希望「陣列（Array）」的元素不會重複，可以使用 `Set`；如果是希望物件（Object）的鍵不會重複，則可以使用 `Map`。

# Set
Set 的特色是有 `has()` 這個方法，可以**快速判斷該 Set 中是否包含某個元素**，==重點不是讓我們把 Set 中的元素取出來用==。

`set` 裡面的鍵不會重複，是 unique 的，每個元素互不相關 (irrelevant)。
類似 `array`，都沒有 key 值，並且是 iterables 的資料型態（可迭代）。
```JavaScript
// new Set Type
let classroom = new Set(); //  建立教室這個 set
let Aaron = { name: 'Aaron', country: 'Taiwan' };
let Jack = { name: 'Jack', country: 'USA' };
let Johnson = { name: 'Johnson', country: 'Korea' };
```

```JavaScript
// 把物件放入 set 中，使用 add 方法
classroom.add(Aaron);

// 檢驗 set 中是否包含某物件，使用 has 方法
if (classroom.has(Aaron)) console.log('Aaron is in the classroom');

// 把物件移除 set 中，使用 delete 方法 
classroom.delete(Jack);

console.log(classroom.size); // 看看 set 中有多少元素
```

常見用法：==過濾陣列中重複的元素==。
利用 Set 中元素不會重複的特性，可以用來過濾掉陣列中重複的元素，留下唯一：
```JavaScript
const arr = [1, 1, 3, 5, 5, 7];
const arrToSet = new Set(arr); // Set { 1, 3, 5, 7 }
const uniqueArray = [...arrToSet]; // [ 1, 3, 5, 7 ]
```

# Map
`Map` 物件是簡單的 key-value 配對，`物件（Object）`和 `Map` 很相似，但是有以下幾點差別：
1. Map 裡面的 **key 是唯一的**，如果 `set` 到重複的 key，則舊的 value 會被覆蓋。
2. `Map` 中的 `keys` 會根據**被添加資料的時間而有順序性**，但 `Object` 沒有順序性。
3. Object 的鍵（key）只能是 `字串（Strings）`或 `Symbols`，而 **`Map` 的鍵可以是任何值**，包含物件、函式或原始型別（primitive type）。
4. 若要取得 `Map` 的大小非常容易，只需要取得 size 屬性即可；而 Object 的大小必須手動決定。
5. 當需要經常增添刪減屬性時，使用 `Map` 的效能會比 `Object` 來得好。

```JavaScript
// 建立 Map
let myMap = new Map(); // 建立空的 Map
let myMap = new Map([
  [1, 'one'],
  [2, 'two'],
]); // 建立 Map 時直接代入內容
```

```JavaScript
// 方法
myMap.has(keyString); // true，透過 .has 判斷該 Map 中是否有某一屬性
myMap.size; //  3，透過 .size 來取得 Map 內的屬性數目
myMap.get(keyString); // 使用 .get(key) 可取得屬性的內容
myMap.delete(keyString); // 刪除 Map 中的某個屬性，成功刪除回傳 true，否則 false
myMap.clear(); // 清空整個 Map
```


# Which Data Strcuture to Use?
DATA 的來源：
1. 程式本身（寫在 code 裡的資料，例如狀態訊息）
2. 使用者介面（透過 DOM 回傳使用者填寫的資料）
3. 外部來源（Web API）
可以用 API 來取得資料

- LIST? (Arrays or Sets)
- Key/Value pairs? (Object or Maps)

Web API 傳回的資料通常是 JSON 格式

使用時機
- Array
  1. 需要排序性（有順序）的資料
  2. 資料中可能會有重複的值
  3. 需要操作 (manipulate) 資料時

- Sets
  1. 需要用到不重複的 unique 資料
  2. 高度注重效能時（舉例來說，搜尋時使用 Sets 的速度會比 Arrays 還快）
  3. 移除陣列 (array) 中的重複值

- Object
  - 傳統的 key/value 儲存方式
  - 方便使用 `.` 和 `[]` 來讀寫資料
  1. 需要包含 function (methods) 時
  2. 用到 JSON 格式時

- Maps
  - 更好的效能
  - keys 可以是任何資料型態
  - 便於迭代 (iterate)
  - 便於計算物件的大小
  1. 只需要 key / value 值時
  2. 當 key 值**不是字串**時

