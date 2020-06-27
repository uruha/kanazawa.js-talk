---
marp: true
theme: uncover
paginate: true
---

<!-- _class: invert -->

# JavaScript を書き始める前に知っておきたい JavaScript のこと #03

Kanazawa.js
Remote Meetup #04

千葉 弘太郎

---

千葉 弘太郎（ちば こうたろう）
Kotaro Chiba

- Twitter: [@ur_uha](https://twitter.com/ur_uha)
- Github: [uruha](https://github.com/uruha)
- Work: DMM.com LLC

---

### 前回

#### JavaScript を書き始める前に知っておきたい JavaScript のこと #02
- 「ざっくり知る」JavaScript の `prototype` について

---

### 今回

- JavaScript の実行順に迫る `イベントループ` の仕組み

---

### JavaScript が実行される環境

`シングルスレッド` で一度に実行できるタスクは1つのみ

---

(´・ω・｀)。o0（じゃあどうやってあんなにたくさんの非同期の処理を実行できてるの？？？）

---

(´・ω・｀)。o0（処理に30秒かかる実行があったら30秒間止まっちゃうんですか...???ﾂﾗｲ...）

---

### 実際は...

1. イベントループ
2. Web API

を駆使して非同期的な処理をしているように見せている。

---

JavaScript は以下のような関係性で処理を行っています。

```
▶️ Call Stack ───────→ ⚙️ Web API

 │                      │
 │                      │
 │                      │

🔄 Event Loop ←──────→ ⏯ Queue
```

---

```js
/** 1 */
function start() {
    return 'start :)';
}
/** 2 */
function asyncFunc() {
    return setIimeout(() => 'exec !', 1000);
}
/** 3 */
function end() {
    return 'end ;)';
} 

start();     // start :)
asyncFunc(); // exec !
end();       // end ;)
```

---

なんとなく  
`1. start :) -> 3. end ;) -> 2. exec !`  
の順で結果が出力されるのは予想できる。

---

なんでかな？

---

```js
/** 1 */
function start() { return 'start :)'; }
```

```
▶️ Call Stack ───────→ ⚙️ Web API
[start()]
 │                      │
 │                      │
 │                      │

🔄 Event Loop ←──────→ ⏯ Queue
```

`start()` は call stack で呼び出されて、  
`start :)` が出力されて終わる（ポップされる）

---
```js
/** 2 */
function asyncFunc() {
    return setIimeout(() => 'exec !', 1000);
}
```

```
▶️ Call Stack ───────→ 🕓 Web API
[asyncFunc()]         [() => 'exec !', 1000sec]
[setTimeout()]          │
 │                      │
 │                      │
 │                      │

🔄 Event Loop ←──────→ ⏯ Queue
```
`asyncFunc()` が実行されて `setTimeout` が callback を WebAPI に追加します。  
`asyncFunc, setTimeout` はこれでポップ。

---

```
▶️ Call Stack ───────→ 🕓 Web API
[end()]         [after 1000sec]
 │                      │
 │                      │
 │                      │

🔄 Event Loop ←──────→ ⏯ Queue
                      [() => 'exec !']
```

1秒後に callback 内の `() => 'exec !'` が queue へ。
call stack 側にはまだ `end()` がいるので、先に `end()` が実行されます。

---

```
▶️ Call Stack ───────→ 🕓 Web API
[() => 'exec !']
 │                      │
 │                      │
 │                      │

🔄 Event Loop ←──────→ ⏯ Queue
```

Event loop が call stack に何も無いことを確認して、  
queue の callback関数を実行します。

---

## まとめ

1. 関数の実行は call stack で
2. 関数の処理によっては Web API を介して callback など queue に待機させる
3. Event loop は call stack と queue を監視している
4. Call stack に実行する関数が無くなった時 event loop が queue に溜まっている関数を call stack へ移して実行

---

### ちょっと詳しく

- Queue にはいくつか種類がある
  - Macrotask
    - `setTimeout | setInterval | setImmediate`
  - Microtask
    - `process.nextTick | Promise callback ...etc`

Event loop が実行する queue の順序は `Microtask > Macrotask` の順

---

## 次回

- どうしようかな... (´・ω・｀)
  - OOPとかをプロトタイプで説明してもちょっと過去の産物になりそうなので、違うネタにする予定
  - なにか要望ありますか？