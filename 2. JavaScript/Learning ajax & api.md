#front-end #JavaScript 
# AJAX/XHR 是什麼？
AJAX 全名 **A**synchronous **J**avaScript **A**nd **X**ML 意即「非同步的 JavaScript 與 XML 技術」，是利用 JavaScript 來跟伺服器進行網路連線的一種技術。

# Fetch
```JavaScript
fetch(網址).then(function(回應物件) {
	console.log(回應物件);
});
```

伺服器會給不同格式的資料，因此需處理不同格式的回應。
1. 純文字
```JavaScript
   fetch(網址).then(function(response){
	   //轉成純文字模式
	   return response.text();
   }).then(function(data){
	   console.log(data); //純文字資料
   })
```
2. JSON 格式
```JavaScript
fetch(網址).then(function(response){
	return response.json();
}).then(function(data){
	console.log(data); //JSON 格式資料/物件陣列結構資料
})
```

JSON格式：
一對中括號代表一個陣列
一對大括號代表一個物件

實例：
```html
<body>

  <h1>AJAX練習</h1>

  <button onclick="getData()">連線取得資料</button>

  <div id="result">

  

  </div>

</body>

  

<script src="https://code.jquery.com/jquery-3.7.0.min.js"

  integrity="sha256-2Pmvv0kuTBOenSvLm6bvfBSSHrUJ+3A7x6P5Ebd07/g=" crossorigin="anonymous"></script>

<script>

  function getData() {

    // 利用 Fetch 連線取得資料

    fetch('https://cwpeng.github.io/live-records-samples/data/products.json').then(function (response) {

  

      //then 後面的函式會接收伺服器回應

      // response 物件會記錄很多回應的資訊

      console.log(response);

      console.log(typeof (response));

  

      return response.json();

    }).then(function (data) {

      // 已經取得資料，把資料呈現到畫面上

      let result = document.querySelector('#result');

      result.innerHTML = '';

      // 利用迴圈逐一讀取陣列資料

      for (let i = 0; i < data.length; i++) {

        let product = data[i];

        // 將資料放到畫面上

        result.innerHTML += '<div>' + product.name + ',' + product.price + ',' + product.description + '</div>';

      }

    });

  }

</script>

  

</html>
```

## Rest
常用到的 CRUD
- POST = 新增
- GET = 讀取資源
- PUT = 替換資源
- DELETE = 刪除資源

PUT 比較正確的定義是 Replace (Create or Update)，例如 `PUT /items/1` 的意思是替換 /items/1，如果已經存在就替換，沒有就新增。PUT 必須包含 items/1 的所有屬性資料。

但是這個行為似乎不怎麼好用，如果只是為了更新`items/1`的其中一個屬性，就需要重傳所有`items/1`的屬性也太浪費頻寬了，所以後來又有新的 [PATCH Method](http://tools.ietf.org/html/rfc5789) 標準，可以用來做部分更新(Partial Update)。