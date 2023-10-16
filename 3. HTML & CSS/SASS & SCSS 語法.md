#CSS 

CSS 預處理器（CSS Preprocessor）透過將程式模組化的概念，新增了變數、巢狀結構、混入、繼承等寫法，作為 CSS 語法的擴充，用以改善程式碼的結構與可維護性。

SCSS 需要使用 `{}` 來包住，並使用分號（;）來結尾。

# 變數 Variables
在 SASS 中可以使用關鍵字 `$` 來建立變數，通常會寫在程式碼最上方，並用於設定按鈕樣式、視覺主色、字型大小等等。
變數的資料型態可以是 Numbers（可以有單位或無單位）、Strings、Booleans、null 值（視為空值），甚至可以使用 Lists、Maps 。

在 SASS 所定義的變數中，**底線（`_`）和連結線（`-`）的使用可以互換**，舉例來說，雖然下面定義的變數名稱是 `$bg_black`，但是一樣可以透過 `$bg-black` 提取：
```SCSS
$bg_black: #333;

.block1 {
  background-color: $bg_black;
}

.block2 {
  background-color: $bg-black;
}
```

### 全域變數（!global）
> [!todo] Todo
>待補充

### 預設變數（!default）
對某一個變數後方加上 `!default` 後，如果這個變數有被賦值過，則使用該值，如果沒有被賦值過，則使用預設值：
```SCSS
// SCSS
$gray: #eaeaea;

$black: #333 !default; // $black 沒被賦值過，所以會套用預設值
$gray: #cacaca !default; // $gray 被賦值過，所以不會套用預設值

.block {
  background-color: $black;
  color: $gray;
}
```
編譯後：
```CSS
/* CSS */
.block {
  background-color: #333;
  color: #eaeaea;
}
```

# 混入 Mixins
將經常被重複使用的程式碼獨立撰寫，以 `@mixin` 語法包裝起來，需要時透過 `@include` 引用，即可根據不同參數來設定相似的樣式，常用於 width、height、flex-center 等。

1. 不帶參數的 mixin
```SCSS
// 經常重複使用的樣式
@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
}

// 需要套用樣式的程式碼
.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
```

2. 帶有參數的 mixin
```SCSS
// 經常重複使用的樣式
@mixin sexy-border($color, $width: 1px) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}

// 需要套用樣式的程式碼
p {
  @include sexy-border(blue);
}
h1 {
  @include sexy-border(blue, 2px);
}
```


# 巢狀 Nesting
基本寫法：
```CSS
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

````col

```scss
// SCSS

nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

```CSS
/* CSS */

nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```
````

