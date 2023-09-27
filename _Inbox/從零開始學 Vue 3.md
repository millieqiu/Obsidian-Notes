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

# Optional API
## Vue 元件的生命週期

## 基本結構
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

-  modelValue
  當在自訂 component 使用 v-model 時，component 接收一個 modelValue 的值，然後透過觸發 `update:modelValue` 事件來更新該值。

### Reactive
如果要宣告結構變數的話就必須要使用 `reactive` ，然後將變數放在裡面，而初始化的時候就不用 `ref` 了。而這個 `reactive` 也必須要 import 才可以使用。
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

### script setup
`script setup` 是 Vue 3 中所提供的語法糖，在 script 標籤加上 setup 就可以了，作用如 `setup()`一樣，所有的變數、函式 都可以直接給模板（template）使用，不需要再 `return`。
