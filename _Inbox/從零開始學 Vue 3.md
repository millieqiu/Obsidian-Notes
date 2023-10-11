# 基本語法

### v-model
實現資料雙向綁定，有以下幾種較常見的修飾符：

- `lazy`：轉為 change 事件後同步
  編輯資料時不會一起更動值，等到輸入完畢離開 input 後才會變動
```html
<!-- HTML -->
<div id="app">
    <input type="text" v-model.lazy="message">
    {{ message }}
</div>
```

- `number`：改變 input 資料型別 typeof
  1. `{{ typeof 資料名稱 }}` 可取得該筆資料的資料型別
  2. 加上修飾符 `.number` 才能改變其資料型態為 number，否則儘管輸入數字也會是 string
```html
<!-- HTML -->
<div id="app">
    <input type="text" v-model="message">
    <input type="text" v-model.number="message">
    <input type="number" v-model="message">
    <input type="number" v-model.number="message">
    {{ message }}
    {{ typeof message }}
</div>
```

```javascript
<script>
	// 假設值為 123456：
    /*
    	欄位一：string
    	欄位二：number
    	欄位三：string
    	欄位四：number
    */
</script>
```

- `trim`：去掉頭尾空格
```html
<!-- HTML -->
<div id="app">
    <input type="text" v-model="message">
    <input type="text" v-model.trim="message">
    首{{ message }}尾
</div>
```

```javascript
<script>
	// 假設值為 " 哈囉 "：
    /*
    	欄位一：首 哈囉 尾
    	欄位二：首哈囉尾
    */
</script>
```

### v-on
事件綁定。

常用修飾符：
- `stop`：阻止點擊事件繼續向上傳播
```html
<div class="one" @click="out">
    <button @click.stop="inside">內層</button>
</div>
```

```javascript
var vm = new Vue({
  el: '#app',
  data: { 
    
     },
  methods:{
    //stop 修飾符
    out(){
      console.log("外層");
    },
    inside(){
      console.log("內層");
    },
  },
})

// 印出結果：
// 內層
```

- `prevent`：取消預設行為，類似 JavaScript 中的 `event.preventDefault()`。

# Functions（功能）

### Filter（過濾器）
Vue 2 中的 Filter 功能在 Vue 3 **已被刪除**，官方建議如果需要做到篩選，可以使用「方法調用（method calls）」或計算屬性「computed」來替代。

常見有兩種方法可以做到篩選功能：
- map：`map` 方法回傳的資料與原來的資料長度相同，數值也做相應處理。
- filter：`filter` 方法則會回傳一組新的資料。
- [?] *map & filter 的差異*

```javascript
let arr = ["1","2","3"];
let a = arr.map((item,index,a) =>{
    return item + 1
});

console.log(a); //["11", "21", "31"]

let b = arr.filter((item,index,a) =>{
    return item > 1
})

console.log(b); //["2", "3"]
```

> [Vue.js 新手如何製作口罩地圖？](https://5xruby.tw/posts/how-to-create-maskmap-by-vuejs-and-osm)
> [如何用 Vue 輕鬆篩選資料與排序](https://hackmd.io/@Zihyin/S1BW60f7q)

# Component（元件基礎）

### slot（插槽）
Slot 是一種內容分發（content distribution）的 API，中文翻譯為插槽，適合用在結構比較複雜，元件內容可以重複使用的地方。簡單說就是==在 component 中可以預留空間，在父層再把內容放進去==。
要在父子元件之間傳遞變數或內容的時候，我們可以使用 props，但如果想要傳遞進去的是一段 template 片段，就要使用到 slot。

![[slot.png]]
如上述例子，Vue 會在子元件的 slot 插入 textNode (#text)，渲染出 `<button>Click Me<button>`。這麼做的好處可以==讓元件變得更彈性==，透過傳入 template 來客製部份元件，所以實際上用到 v-slot 的狀況，通常不會只傳入簡單的文字內容。

#### 具名插槽
有時候我們會遇到一個元件裡有好幾個 slot 出口的狀況。以下面的 `<BaseLayout>` 為例：
```html
<!-- component 子層 -->
<div class="container">
  <header>
    <!-- 標題內容放這裡 -->
  </header>
  <main>
    <!-- 主要内容放這裡 -->
  </main>
  <footer>
    <!-- 底部内容放這裡 -->
  </footer>
</div>
```
對於這種場景，`<slot>` 元素可以有一個特殊的屬性「`name`」，用來給各個插槽分配唯一的 ID，以確認每一處要渲染的內容。
```html
<!-- component 子層 -->
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```
這類具有 `name` 屬性的插槽則稱為「具名插槽」。要為具名插槽傳入內容，我們需要在 `template` 標籤上運用 `v-slot` 指令：
```html
<!-- App 父層引用元件 -->
<BaseLayout>
  <template v-slot:header>
    This is a header
  </template>
</BaseLayout>
```
![[named-slot.png]]
**要注意 `v-slot` 只能添加在 `<template>` 上**。

### 動態元件
有些場景會需要在兩個元件間來回切換，例如常見的 Tab 介面。


### 狀態保留 keep-alive
`<keep-alive>` 是 Vue 的內建元件，它的功能是在多個元件動態切換時暫存狀態。

在預設情況下，一個元件被替換掉後就會變銷毀，導致它丟失所有已變化的狀態，而當這個元件再次被顯示時，只會創建帶有初始狀態的新實例。
若我們希望元件被切換走後還能保留剛才被改變的狀態，就可以使用 `<keep-alive>` 來達成，將動態組件包裝起來：
```vue
  <keep-alive>
    <ComponentThree v-if="tab === 'tab3'" />
  </keep-alive>
```


# Vue 的生命週期
一個 Vue.js 的網頁應用程式是由各種大小的元件組成，而每個 Vue 的實體物件，實際上就是一個元件，而每個元件從建立到被銷毀，都有它的生命週期階段。

Vue 實體的生命週期為：
建立（Creation）➡️ 掛載（Mounting）➡️ 更新（Updating）➡️ 銷毀移除（Unmounting）

*以下為 Vue 3 的寫法：*
1. Creation：元件開始被建立的階段
   - `beforeCreated()`：Vue 實體被建立，狀態與事件都尚未初始化
   - `created()`：Vue 實體被建立，狀態與事件都尚未初始化
```
適合用於呼叫 API
```

2. Mounting：直到 Vue 完成元件跟 DOM 掛鉤，可以被渲染到 HTML 頁面上的階段
   - `beforeMount()`：Vue 元件尚未與 DOM 掛鉤
   - `mounted`：Vue 元件掛載完成

3. Updating
   - `beforeUpdate()`：當狀態被變動時，畫面同步更新前
   - `updated()`：當狀態被變動時，畫面同步更新完成

4. Unmounting
   - `beforeUnmount()`：Vue 元件被銷毀前
   - `unmounted()`：Vue 元件被銷毀完畢


# Optional API

### 基本結構
```javascript
export default {
  props: {},
  data() {
    return {};
  },
  watch: {},
  computed: {},
  methods: {},
};
```
Vue 2 的 Optional API 寫法，雖然很簡單易懂，但隨著專案複雜度提高，程式碼會不斷膨脹，後續的維護成本會逐漸增加；大量使用 `mixins` 時也容易使命名出現衝突、程式來源不清等問題。

---
# Composition API

### Composition 生命週期
組合式 API 的生命週期函式又有不同的寫法如下：
```javascript
import { onMounted, onUpdated } from 'vue'
export default {
  name: 'HelloWorld',
  setup() {
    onMounted(() => console.log('Mounted'));
    onUpdated(() => console.log('Updated'));
    // ...
  }
}
```
至此，就==沒有 Creation 階段的 Hook Functions 了==，改用 **`setup()`** 來取代，在 `setup()` 這個函式通常會包含生命週期鉤子。
而在 `setup()` 函式的最後，必須要把給模板解析的內容（包含狀態與事件處理方法等）透過 `return` 回傳出去。

Composition API 與 Optional API 最大的差別，就是在元件的實體物件內已經不會再有 data、computed、methods 與生命週期 Hooks 等屬性。

**Composition API 改善的問題**：
-  程式能依功能分類使用，增加可讀性；
-  封裝功能，可跨元件使用，增加複用性；
-  提供更好的 TypeScript 支持。

### 入口函式 Setup
全新的 [`setup`](https://v3.cn.vuejs.org/api/options-composition.html#setup) 選項為一個函式，它會在元件實體尚未被建立**之前**執行，是使用 Composition API 實際位置。

### Ref
可以把 `ref` 想成就是 Vue 2 時的 `data`。
```javascript
// Vue 2 寫法
data(): {
  msg: 'Hello World'
}
```

使用 Composition 宣告變數要用 `ref` 來初始化，而這個 **`ref` 必須要先 import 才可以使用**。
```javascript
// Vue 3 寫法
import { ref } from 'vue';

export default {
	setup() {
		  const msg = ref('Hello World');
		  return { msg }
	}
}
```

修改 `ref` 的值時必須使用 `.value`，因為 `ref` 會將該變數轉換成一個響應式的物件(意指 Proxy 物件)，因此若要修改的話則必須透過 `.value` 的方式。

-  modelValue
  當在自訂 component 使用 v-model 時，component 接收一個 modelValue 的值，然後透過觸發 `update:modelValue` 事件來更新該值。

### Reactive
如果要宣告結構變數的話就必須要使用 `reactive` ，==針對物件或陣列做雙向綁定監聽==，然後將變數放在裡面，而初始化的時候就不用 `ref` 了。而這個 `reactive` 也必須要 import 才可以使用。
``` html
<template>
  {{ user.id }} {{ user.name }}
</template>
```

```javascript
<script>
import { reactive } from 'vue';

export default {
  name: 'App',
  setup() {
    const user = reactive({
      id: 0,
      name: '',
    });

    user.id = 1;
    user.name = 'Allan';

    return {
      user,
    };
  },
};
</script>
```

### toRef

### toRefs


### script setup
`script setup` 是 Vue 3 中所提供的語法糖，在 script 標籤加上 setup 就可以了，作用如 `setup()`一樣，所有的變數、函式 都可以直接給模板（template）使用，不需要再 `return`。

### 函式
函式的宣告直接宣告在 `setup() {}` 即可。
