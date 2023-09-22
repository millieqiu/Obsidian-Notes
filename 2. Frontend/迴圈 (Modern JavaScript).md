# For of loop
ES6 有了 `for-of` 語法，這大概就是結合 `forEach` 可以直接得到元素的好處，外加 **`for` 可以用 `break`、`continue` 做到更彈性操作**。
```JavaScript
const arr = ['a', 'b', 'c'];
arr.prop = 'property value';

for (const elem of arr) {
  console.log(elem);
}
// Output:
// 'a'
// 'b'
// 'c'
```
現在你可以在 `for-of` 中直接得到元素了，並且裡面可以使用 `await`，你也可以提早中斷迴圈。

# Enhanced Object Literals
平常我們用大括號 (`{}`) 來建立物件的語法，就稱為物件實字 (Object Literals)。
物件實字的語法重點：
- 用大括號表示。
- 裡面的**屬性 (Properties)** 用**名值對 (name-value pairs)** 表示。
- 多個屬性以逗號 (comma) 分隔。
- 宣告完後，還是可以再增加 Properties 進去。

ES6 支援一些新的語法，讓物件實字能夠更簡潔、靈活。
1. 物件屬性初始化的語法簡寫
```JavaScript
function getPlayerObj(name, progress){
    return {
	    name: name,
		progress: progress
	};
}

console.log( getPlayerObj("OneJar", 23) );   // {name: "OneJar", progress: 23}
```
我想把變數 `name` 和 `progress` 作為物件屬性 `name` 和 `progress` 的初始值，變數名稱和屬性名稱碰巧一模一樣。
在 ES5 以前，必須把**屬性名稱**和**進行賦值的變數名稱**都標明清楚。
對於這種「**屬性名稱**和**進行賦值的變數名稱**一模一樣」的情境，ES6 提供了更簡潔的語法：
```JavaScript
function getPlayerObj(name, progress){
    return {
	    name,
		progress
	};
}

console.log( getPlayerObj("OneJar", 23) );   // {name: "OneJar", progress: 23}
```

2. 物件函式的語法簡寫
ES5 以前，物件函式的宣告方式就是使用 `function` 關鍵字進行函數的定義：
```JavaScript
function getPlayerObj(name, progress){
    return {
        sayHi: function(){
		   return `Hi, I am ${name}`;
	    }
	};
}

console.log( getPlayerObj("OneJar", 23).sayHi() ); // "Hi, I am OneJar"
```
ES6 支援更簡潔的寫法，省略了 `function` 關鍵字和冒號 `:`，將簡寫語法所定義的物件函式，定義為**傳統函式**：
```JavaScript
function getPlayerObj(name, progress){
    return {
        sayHi(){
		   return `Hi, I am ${name}`;
	    }
	};
}

console.log( getPlayerObj("OneJar", 23).sayHi() ); // "Hi, I am OneJar"
```

3. 具運算性的屬性名稱
ES6 直接在物件實字的語法內增加可運算的特性，算是提供了另一種語法選擇：
```JavaScript
var prefix = "lng";
var i = 0;

var player = {
    [prefix + (++i)]: "JavaScript",
    [prefix + (++i)]: "Java",
    [prefix + (++i)]: "C"
};

console.log(player); // {lng1: "JavaScript", lng2: "Java", lng3: "C"}
```


Object.keys() & Object.values() & Object.entries()
*(待補充)*