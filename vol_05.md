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

Mutable な変数を定義した場合、  
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
    - Symbol `(ES6~)`
    - BigInt `(ES10~ new)`
- Object

---

### プリミティブ型
JavaScript の情報において一番低いレイヤの単位。

これ以上別の型には分解できません。

対局に `Object型` が存在します。

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
  - `Number.MAX_SAFE_INTEGER (9007199254740991)` で取得可能
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

- ES10(ES2020) で策定
- `Number.MAX_SAFE_INTEGER` 以上の数値を安全に扱える
- Number と混同して仕様することができない

---

#### Boolean
```js
const thisIsTrue = true;

const thisISFalse = false;
```

---

#### Undefined
```js
const unDefined;
console.log(unDefined); // undefined

const obj = {};
console.log(obj.foo); // undefined
```

以下の時に自動的に割り当てられます。

1. 宣言されている変数に値が割り当てられていない
2. 任意のオブジェクトのプロパティが定義されていない

---

#### Null
```js
const nullnull = null;
```

`undefined` と違い、明示的に値を割り当てていないことを宣言します。

また、その変数などは今後別の値が割り当てられることを示唆していることも意味します。

---

#### Symbol
```js
const newSymbol = Symbol('new symbol');
newSymbol.toString(); // => 'Symbol(new symbol)'
newSymbol.description // => 'new symbol'

const preSymbol = Symbol('new symbol');
newSymbol === preSymbol // => false
```

`Symbol` を宣言する値は、固有のID(シンボル)を持つ値として区別されます。

上記のようにシンボルには任意の `description` を宣言できますが、内容が同じでも一度作成したシンボルは固有のものとして存在するため比較をしても `false` が返ります。

---

### 値の生成

リテラルとコンストラクタ関数の宣言で行えます。

コンストラクタ関数に `new` 演算子をつけて宣言すると Object型になるので注意しましょう。

---

```js
// Literal
const literalNum = 'stringggggggggg';

// Constractor
const constractorNum = String('stringggggggggg');

// Object
const newString = new String('stringggggggggg');

typeof literalNum     // => string
typeof constractorNum // => string
typeof newString      // => object
```

---

### 値の比較

プリミティブ型の値は「値そのもの」を比較します。

比較には `同値` `等値` の2種類が存在します。

---

```js
// 同値
1    === 1             // true
1    === '1'           // false
1    === new Number(1) // false
null === undefined     // false

// 等値
1    == 1             // true
1    == '1'           // true
1    == new Number(1) // true
null == undefined     // true
```

- `同値`: 型と値、両方を比較
- `等値`: 値を比較し型はスルーする

---

### まとめ

- JavaScript のデータ型にはプリミティブ型とObject型がある
  - プリミティブ型は現在7種類
- 型から値を生成するにはリテラルとコンストラクタ関数を用いて行える
- プリミティブ値は「値そのもの」を比較できる
  - `同値` `等値` の2種類の比較ができる

---

### 次回
データ型をもう少し詳しくやっていき！