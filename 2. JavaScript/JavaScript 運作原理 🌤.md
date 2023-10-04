#front-end #JavaScript 
- 高階語言
  不像 C 語言一樣需要管理電腦資源，高階語言如 JS 或 Python 等，可以幫助我們輕易地讀取、撰寫與學習，然而它的缺點就是速度與優化性能無法如 C 語言一樣快。
  
- 垃圾回收機制
  自動移除電腦記憶體中舊的被刪除的或者不重要的資料。
  
- 即時編譯
  將程式語言轉換成機器語言的過程叫做「編譯」，JS 則將編譯器放在內部引擎裡。
  
- 多重語言 (?)

- 基於原型的物件導向

- 高階函式
  將函式視為一種變數，可以將函式傳遞給函式，也可以從其他函式裡 return 函式。
  
- 動態程式語言
  宣告變數前不用定義型別，資料的型別就會自動改變。在其他程式語言如 C#、Java 中，必須提前宣告型別，同時也能預防錯誤。
  
- 單執行緒
  a single-threaded non-blocking async concurrent language.
  單執行續的程式語言，根據這裡的解釋：意思就是一次只能做一件事情，如果安排了很多事情要給他做，他就會讓這些事情去**排隊**，再一件一件做，逐步執行。這也就是所謂的同步。也就是**一次只做一件事情**。
  可以透過瀏覽器提供的第三方 WebAPI (ex: document、XMLHttpRequest、setTimeout) 給我們使用，來做到**不同步處理**。
  
- Non blocking event loop


在開始之前，先來聊聊我們撰寫的程式語言要如何跟電腦溝通。
JavaScript 引擎的工作就是把人類語言轉換成機器看得懂的語言，如同類似的電影中人類和外星人交流一樣。
在 Coding 的世界裡，通常有兩種方式用來翻譯機器語言，分別是「直譯」和「編譯」。
- 直譯器：
  如果透過直譯器，程式語言便會一行一行邊解釋邊執行。
- 編譯器：
  編譯器則會一次把所有程式語言翻譯成機器語言，執行時就不再需要翻譯的動作。
直譯器的好處是執行和啟動的速度快，不需要等待整個編譯過程完成就可以執行程式，對於 Web 開發人員來說，這種方式更適合 JavaScript，因為我們需要即時瀏覽程式的結果，因此早期的 JS 都是採用直譯的方式運作。
然而，比方說執行一個 loop，直譯器就得重新一行一行翻譯，卻也導致效率低下。

後來衍伸出了 Just-in-time (JIS)，也就是**即時編譯**，綜合兩者的優點，在 JavaScript 引擎中加入監視器，並仰賴一個能夠編譯並且執行產生結果的環境，也就是所謂的 JS 引擎。

## JavaScript Runtime
JavaScript 的 Runtime 包含 JS Engine (核心概念，包含 Heap 和 Call Stack) + Web API (DOM、Timer、Fetch API 等) + Callback Queue (例如 click 等)。
當我們觸發一顆按鈕的 click 事件，事件會觸發一個 funciton，這個 funciton 也就是所謂的 callback function。callback func 被放進 callback queue 中，等到引擎中的 call stack 清空，這個函式就會被移到 callback queue 裡面等待執行。

【名詞解釋】
* Heap：主要是進行記憶體的分配，存放**物件型別**的資料。
* Call Stack：JavaScript 中等待執行的任務會放入這裡，儲存基本型別的資料。
* Event loop：Event loop 顧名思義就是一個 loop，做的就是一直在觀察 Calling Stack 是否空了，如果空了就把排隊中的 callback 按照順序推進 Call stack。
* Callback queue：這裡放置的 Task 有較高的優先權。Event Loop 會優先檢查及執行 Job Queue 裡的 Task，全部執行完後才會到 Callback Queue 看有沒有其他隊列的事件要執行。


![[js-runtime.png]]


Call Stack 裡包含很多個執行環境 (Execution Context)
>**執行環境**是一個抽象的概念，概括地來說，任何你JS 程式碼被執行、讀取的地方，像是 function 裡、甚至全域 ，都可以是執行環境。執行環境可以分為以下幾種：
>1. Variable Environment
>2. Scope chain
>3. this keyword

- 全域執行環境 (Global Execution Context)：
在執行任何程式之前，預設會建立的一個全域環境。  
全域執行環境替我們做了兩件事情：  
a. 建立全域物件 (Global object)，以 web browser 來說就是 window  
b. 建立「this」
- 函式執行環境 (Function Execution Context)：
在函式執行 (invoke) 的時候會各別為函式建立專屬的執行環境，  執行一個函式就會建立一個該函式的執行環境，所以有可能同時會有多個函式執行環境。

### Scope
Scope 定義了變數的可及與可視範圍，可稱為作用域 / 範疇 / 生存範圍 / 存在範圍，意思是變數可以被取用 (accessibility)，或者可以被看到 (visibility) 的有效範圍。
#### 3 Types of Scope

1. Global Scope 全域變數
   Global Scope 意即不在函式或區塊內宣告的變數，可以在任何地方取用變數的範圍。
2. Function Scope 函式作用域
   在函式內宣告的變數，僅在函式內可取用，也被稱作 Local Scope。
```JavaScript
 function calcAge(birthYear) {
	 const now = 2023;
	 const age = now - birthYear;
	 return age;
   }
   console.log(now); //ReferenceError
```
3. Block Scope (ES6) 區塊作用域
   區塊的意思就是大括弧 (curly brace) `{}`，只有在這個大括弧內才可取用。（僅適用於 `let` 跟 `const`）
   如果剛剛的範例中以 `var` 來宣告，則會發現在大括弧外一樣可以取用變數，因為 **var 不是區塊作用域，而是函式作用域**。

==語彙範疇 Lexical Scope==
又稱為靜態範疇 (Static Scope)，意指在我們打好程式碼進行編譯時，作用域就已經依我們程式碼的內容決定好了。相對於語彙範疇則有動態範疇 (Dynamic Scope)，Javascript 與大多數的語言多採用靜態範疇，動態範疇的語言則要直到程式執行該位置才能決定作用域。
並語彙範疇 (Lexical Scope) 具有一個特性：**裡面的可以拿外面的，外面的不能拿裡面的**，意思是如果 func A 包著 func B，各具有各自的變數，裡面的 func B 可以拿到外面 func A 的變數，A 拿不到 B 的。


>TL;DR
>Scope 是變數的取用範圍，而程式的詞彙環境 (Lexical Environment) 決定了這個範圍，Javascript 引擎會依著範圍鏈 (Scope chain) 尋找可取用的變數。
>Javascript 為靜態範疇 (Lexical Scope)，所以在程式執行的時候就已經決定了所有變數的 Scope。

### Hoisting
簡單記憶 Hoisting 的概念：「**幫你留位子**」，因為 Hoisting 就是 **Javascript 在執行任何程式碼之前，先把宣告的變數和函式放進記憶體空間裡**，就像是事先幫他們留個位子的感覺。
不同資料型態的 hoisting 狀況：
1. function declaration
   - hoisted?: yes; 初始值: actual function
2. var
   - hoisted?: yes; 初始值: undefined
3. let, const
   - hoisted?: no (Technically, yes, but not in practice) ; 初始值: uninitialized, TDZ
4. ==function expression & arrow function==
   - 根據他們是如何被宣告而決定 (var or let, const)

更精準一點說，let & const 在宣告時其實**有**被提升，但是跟一般以 var 宣告變數的提升方式不太一樣，差別在於 let & const 提升後在未被初始化 (Initialization) 之前不可使用，意思就是 let const 宣告之後，在賦值之前，不能被取用。
#### Temporal Dead Zone (TDZ)
在 let & const 宣告後未被賦值之前不可取用的期間，我們就稱為「暫時死區(Temporal dead zone)」，在這期間如果要取用 let & const 宣告的變數，Javascript 會回傳 `ReferenceError` 的錯誤。
1. 在 ES6 中新增的屬性，能夠讓我們更輕鬆地避免錯誤和除錯。
2. 讓 const 能夠依照設定的方式運作（如果因為 hositing 的特性先將 const 宣告為 undefined 後又賦予值，則違反了 const 不能重複宣告的原則）。

Hoisting 的好處：
1. 在 function 宣告前就可以使用該函式，增加函式運用上的可讀性。
2. var variable 的 hoisting 特性可說是跟著 function 被一起創造出來的副產品而已（？）

【Example】
```JavaScript
if (!numProduct) deleteShopptingCart();

var numProduct = 10;

function deleteShoppingCart() {
	console.log('All products deleted!');
}

//執行結果: All products deleted!
```
由於 var 宣告的變數先**提升成 undefined**，因此儘管下面宣告 numProduct 為 10，一樣會執行 deleteShoppingCart 的函式。
解決方法：
1. 不使用 var 進行宣告，盡量以 const 來宣告，若真的需要設定變數則使用 let
   var 為全域作用域，因此會將資料宣告在 ==window 物件==裡，讓整個 web page 都可讀取
2. 將所有宣告式放在 Scope 最上方

## this keyword
每個執行環境 (execution context) 創造出的特殊變數，會根據函式是**如何被呼叫**的而有所不同。
1. method 👉 this = Object that is call the method
2. simple function call 👉 this = 在瀏覽器底下會是 `window`，但在 strict mode 裡會是 `undefined`
3. arrow function 👉 this = this of surrounding function (lexical this 根據父層 scope 來決定) bcs **arrow function don't get its own this keyword**
4. Event Listener 👉 this = DOM element that the handler is attached to
除了上述幾點重要的規則，可以使用 new, call, bind, apply 來創造 this keyword *(待補充)*
![[this-obj-method.png]]

【Example】
```JavaScript
const millie = {
	firstName: Qiu,
	greet: () => console.log(`Hi, ${this.firstName}`),
}

millie.greet(); //Hi, undefined
```
由於 greet 箭頭函式不會創造自己的 this keyword，因此會指向父層的 scope 也就是 global scope，在嚴格模式底下回傳 this 為 undefined。
✏註記：為何 this 不是指向 millie 這個 Object？首先要知道的是，Object 的大括號只是宣告物件所需要的寫法，並不會創造一個 Scope，因此這裡的 this 不會指向 millie 物件。

## Primitive & Object/Reference Type
先上例子：
```JavaScript
let age = 22;
let oldAge = age; //原因: oldAge 在這個階段就被宣告為 22 了
age = 23;
console.log(oldAge, age); // 22 23
```

另一種情況：
```JavaScript
const me = {
	name: 'Jane',
	age: 22,
};

const friend = me;
friend.age = 25;

console.log(friend.age); //25
console.log(me.age); //25
```

同樣都是複製並重新宣告資料，為什麼結果會不一樣呢？
在 Javascript 中，參數的傳遞分為「**傳值**」和「**傳址**」兩種方法：
- 傳值可稱為 Call by value 或 Pass by value
- 傳址則稱為 Call by reference 或 Pass by reference，或是有時候也會聽到的「傳參考」

當一個變數被賦予基本型別的值時，整個值就會存在記憶體裏。當我們要拷貝基本型別的值到另一個變數，我們只會拷貝它們的**值**，而該兩個變數並不會影響到對方。這個情況稱為**傳值 (pass by value)**。

但物件型別的存取方法就不同了。當變數被賦予的是**物件型別**的資料，記憶體會存放該物件在記憶體中的地址，並引**用該地址來指向該物件**。
具體來說，如果變數的值是物件型別，棧內存 (stack) 會存放該物件在堆內存 (heap) 的地址，並引用該地址來指向該存放在堆內存 (heap) 的物件。
所以，當我們要拷貝一個物件到另一個變數時，我們拷貝的是**該物件的地址**，換言之，如果物件有被修改，所有引用該物件地址的變數，它們的值都會被修改。

![[js-memory.png]]

### 深拷貝 v.s. 淺拷貝
既然物件型別是傳參考，那我們該如何複製物件呢？
分成兩種複製方法：
1. 淺拷貝
2. 深拷貝

#### 淺拷貝
假如物件內還有物件，就算使用了淺拷貝，第二層物件還是指向相同的記憶體位置。

#### 深拷貝
深拷貝就是完全複製一份，不會有共用記憶體的問題。

常見深拷貝物件方法有：

- 利用 JSON 方法：先轉 JSON 格式，再轉回來。
- 使用第三方函式庫：
    - jQuery 的 [`$.extend()`](http://www.html.cn/jqapi-1.9/jQuery.extend/)
    - Lodash 的 [`_.cloneDeep()`](https://www.lodashjs.com/docs/lodash.cloneDeep)
