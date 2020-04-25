---
marp: true
---

<!-- theme: uncover -->
<!-- _class: invert -->
<!-- paginate: true -->

# JavaScript を書き始める前に知っておきたい JavaScript のこと

Kanazawa.js
Remote Meetup #02

千葉 弘太郎

---

千葉 弘太郎（ちば こうたろう）
Kotaro Chiba

- Twitter: [@ur_uha](https://twitter.com/ur_uha)
- Github: [uruha](https://github.com/uruha)
- Work: DMM.com LLC

---

前回

[JavaScript を書き始める前にやっておきたいこと](https://speakerdeck.com/uruha/kanazawa-dot-js-meetup-number-1)

---

今回

- JavaScript の歴史
- JavaScript とは

---

## JavaScript の歴史

---

- 1995 ~ LiveScript (Brendan Eich from Netscape)
  - 初期は LiveScript として開発された。後にその当時 Java が流行っていたことから、現行の JavaScript の命名となる
- 1996 ~ Internet Explorer 3.0 搭載
  - これ以降ブラウザによってJSの実装 (仕様) がことなるため非常にこれが問題になる「ブラウザ問題」

---

- 1997 ~ ECMA international 発足
  - JavaScript の標準仕様である ECMAScript (通称ES) が定義される
    - TC39 (Technical Committee) という専門委員会が策定
    - 現在は ES5 がメジャーで最新は ES9 まで標準化が動いている

---

- 2000 ~ 発展
  - Google, Amazon が積極的に JavaScript を使用したWebサービスを展開
  - **Ajax** の誕生・**Google map** のサービス開始などで世間に衝撃を与える
    - 今では当たり前の技術として普及

---

- 最近 ~ より便利なWebの世界に
  - ECMAScript 更新が活発化 (先述)
    - ブラウザの機能を拡張する Web API の提供などが注目されている
      - Web VR
      - Web RTC
      - Web Bluetooth
      - Shape Detection

---

## JavaScript とは

---

### JavaScript と ECMAScript の関係

- ECMAScript は [ECMA International](http://www.ecma-international.org/default.htm) によって標準化されている **JavaScript の仕様** を指す
- ECMA International では ECMAScript を管理番号として `262` と定めており、 `ECMAScript` と `ECMA-262` は同じ意味になる

---

イメージ

```
仕様 (ECMAScript) => 実装 (JavaScript)
```

---

## JavaScript の特徴

- 軽量な**インタープリタ**型プログラミング言語
- または、実行時コンパイルされる、**第一級関数**を備えたプログラミング言語とも言える
- Client で**DOMの操作**が行える

---

### インタープリタ

- コードが上から下に実行されてコードの実行結果がすぐに返ってくる原理
  - スクリプトを実行する際にコンパイルされてバイナリとして実行される
- JavaScript は JIT (just-in-time compiling) という技術を用いて、 実行時の最適化を図っている

---

| エンジン名 | 言語 | その他 |
| --- | --- |:--- |
| Spider Monkey | C | JS開発当初のエンジン |
| Rhino | Java | Node.js より前のサーバサイド側のエンジン |
| V8 | C++ | Chrome などのブラウザでのJS実行エンジン |
| Node.js | C++ | サーバサイドでJSが実行できるエンジン |

---

### 第一級関数

- 定義した関数が変数 (オブジェクト) として扱うことができる言語仕様

---

```js
function sayHello() {
   return "Hello, ";
}

function greeting(helloMessage, name) {
  console.log(`${helloMessage()}${name}`);
}

// `sayHello` を `greeting` 関数の引数として渡す
greeting(sayHello, "JavaScript!");
```

> - 参考: [MDNより](https://developer.mozilla.org/ja/docs/Glossary/First-class_Function)

---

## DOM 操作

- DOM (Document Object Model) にアクセスができる
  - テキストの更新
  - タグ要素の追加・削除・移動
  - スタイルの更新もできる
  - jQuery は DOM の操作に特化
  - etc...

---

```html
<!-- 初期状態 -->
<div>
    <p>Hello World !</p>
</div>
```
```js
// 上記のDOM構造に対して以下の処理を実行
const paragraph = document.getElementsByTagName('p');
paragraph[0].textContent = 'Hello New Wolrd !!';
```
```html
<!-- 上記の処理で以下になる -->
<div>
    <p>Hello New Wolrd !!</p>
</div>
```

---

## まとめ

- JavaScript
  - そんなに歴史は長くない
    - 仕様が乱立して、ECMAが今は取り纏めている
    - 最近はクライアント・サーバサイド共によく使われている
  - インタープリタ型で第一級関数を持つスクリプト言語
    - 言語が実行される際にコンパイルされる
    - 関数を変数などで扱うことができる
    - DOM の操作もできる

---

## 次回予告 (参加できたら)

---

### JavaScript を書き始めたら知っておきたい JavaScript のこと

- JavaScript についてもう少し詳しく
  - オブジェクト指向
  - prototype 継承
  - 動的型付け
  - シングルスレッド