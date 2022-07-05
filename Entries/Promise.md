# JavaScript Promise

## Promise とは
非同期処理を抽象化したオブジェクトとそれを操作する仕組みのこと。

### 使い方
1. `new Promise(fn)` の返り値が promise オブジェクト
2. `fn` には非同期の何らかの処理を書く
	- 処理結果が正常なら、`resoolve(結果の値)` を呼ぶ
	- 処理結果がエラーなら、`reject(Errorオブジェクト)` を呼ぶ

### コツ
#### `thenable` なオブジェクトをラップする
```javascript
$.ajax("https://example.com"); // => `.then` を持つオブジェクト

const promise = Promise.resolve($.ajax("https://example.com")); // => promise オブジェクトへ
```

#### 同期と非同期は混在する
下記の例は、配置する場所によってコンソールに出てくるメッセージの順番が変わる
```javascript
function onReady(fn) {
    const readyState = document.readyState;
    if (readyState === "interactive" || readyState === "complete") {
        fn();
    } else {
        window.addEventListener("DOMContentLoaded", fn);
    }
}
onReady(() => {
    console.log("DOM fully loaded and parsed");
});
console.log("==Starting==");
```

非同期コールバックは、決して同期的に使ってはならない。適したスケジューリングを行うには、 `setTimeout` のような非同期 API を用いる(上記の例で言えば、`fn()` ではなく `setTimeout(fn, 0)` とする)。

#### `.then` は常に新しい promise オブジェクトを返す
`.then` のメソッドチェーンは一見トップのオブジェクトに処理を書いているように見えるが、実際には新しいオブジェクトが返されている。
したがって以下の例はアンチパターン。
```javascript
function badAsyncCall() {
    const promise = Promise.resolve();
    promise.then(() => {
        // 何かの処理
        return newVar;
    });
    return promise;
}
```

正しくは
```javascript
function anAsyncCall() {
    const promise = Promise.resolve();
    return promise.then(() => {
        // 何かの処理
        return newVar;
    });
}
```

#### `Promise.all` と `Promise.race`
all は言わずもがな、race は any みたいな。