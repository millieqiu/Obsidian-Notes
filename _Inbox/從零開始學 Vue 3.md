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

```javascript
// Vue 3 寫法
setup() {
  const msg = ref('Hello World');
  return { msg }
}
```

-  modelValue
  當在自訂 component 使用 v-model 時，component 接收一個 modelValue 的值，然後透過觸發 `update:modelValue` 事件來更新該值。

