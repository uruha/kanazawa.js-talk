---
marp: true
theme: uncover
paginate: true
---

<!-- _class: invert -->

# JavaScript を書き始める前に知っておきたい JavaScript のこと #04

Kanazawa.js
Remote Meetup #05

千葉 弘太郎

---

千葉 弘太郎（ちば こうたろう）
Kotaro Chiba

- Twitter: [@ur_uha](https://twitter.com/ur_uha)
- Github: [uruha](https://github.com/uruha)
- Work: DMM.com LLC

---

### 前回

#### JavaScript を書き始める前に知っておきたい JavaScript のこと #03
- JavaScript の実行順に迫る `イベントループ` の仕組み

---

### 今回

- JavaScript の `データ型` について知ろう（プリミティブ型編） ！

---

JavaScript は `動的型付け` の言語

---

```js
let mutableVar = 'Hello'; // => String Type
    // substitution
    mutableVar = 42;      // => Number Type
    // substitution
    mutableVar = true;    // => Boolean Type
```

---

Mutable な変数を定義した場合（ `const` は原則できない）、  
動的にその変数の型を変更することができる。

---

＿人人人人人人人人人人人人人人人人人人人人人＿
＞　JavaScript にも型はあります　＜
￣Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y￣

---

## 型の種類

---

- `プリミティブ型`
    - String
    - Number
    - Boolen
    - Undefined
    - Null
    - Symbol `(ES6)`
    - BigInt `(ES10 new)`
- Object

---

### プリミティブ型
JavaScript の情報において一番低いレイヤの単位。

これ以上別の型には分解できません。対局に `Object型` が存在します。

プリミティブ型の値を `プリミティブ値` と言います。

---

## プリミティブ型の紹介

---

#### String
```js
const str = 'Hello World :)';
```

- 16 ビット符号なし整数値の **要素** の集合体
- 各要素は文字列の位置を指します
  - `'Hello World :)'` では最初の文字を index 0, 次を index 1... とする

---

#### Number
```js
const num = 1919;
```

- 「倍精度 64 ビット形式による IEEE 754 値」 (-(2^53-1) から 2^53-1 の間の**数値**)
  - `Number.MAX_SAFE_INTEGER` で取得可能
- 『整数』というわけではないでないことに注目！
- これより大きい数値を扱いたい場合はどうすれば...

---

#### BigInt
```js
const bigNum = 2n ** 54n;
// 18014398509481984n
const morebiggerNum = bigNum + 100n;
// 18014398509482084n
```

- `Number.MAX_SAFE_INTEGER` 以上の数値を安全に扱える
- Number と混同して仕様することができない

---

#### Boolen
```js
const thisIsTrue = true;
const thisISFalse = false;
```

---

#### Undefined, Null
```js
const unDefined;
const nullnull = null;
```

## 値の生成

---

---

## 値の比較

---
