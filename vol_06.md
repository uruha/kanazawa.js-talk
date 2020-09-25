---
marp: true
theme: uncover
paginate: true
---

<!-- _class: invert -->

# JavaScript を書き始める前に知っておきたい JavaScript のこと #05

Kanazawa.js
Remote Meetup #06

千葉 弘太郎

---

千葉 弘太郎（ちば こうたろう）
Kotaro Chiba

- Twitter: [@ur_uha](https://twitter.com/ur_uha)
- Github: [uruha](https://github.com/uruha)
- Work: DMM.com LLC

---

### 前回

#### JavaScript を書き始める前に知っておきたい JavaScript のこと #04
- JavaScript の `データ型` について知ろう（プリミティブ型編） ！

---

### 今回

- JavaScript の `データ型` について知ろう（オブジェクト編） ！

---

おさらい

---

- `プリミティブ型`
    - String
    - Number
    - Boolen
    - Undefined
    - Null
    - Symbol `(ES6~)`
    - BigInt `(ES10~ new)`
- `Object` <= 今日はこれ

---

### オブジェクト (複合型)
1つ以上のプリミティブ値を格納できるレイヤ。

プリミティブ値と違い、メモリサイズを特定できない。

`複合オブジェクト` `参照型` とも呼ばれる。

---

「複合」はわかるけど、なぜ「参照」🤔

---

```js

const obj_01 = {};
const obj_02 = obj_01;
obj_01.foo = 1;

console.log(obj_01.foo, obj_02.foo);
// => 1, 1

```

---

🤔🤔🤔

---

生成されたオブジェクトを操作する場合、
オブジェクトのコピーは値をコピーするのではなく、
**「参照先」をコピーする。**

🙋‍♀️ cf. プリミティブ値は値そのものが渡される

---

また、オブジェクトのプロパティは**動的に更新が可能。**

⚠️ 参照先を共有しているオブジェクト自体のプロパティが更新されると全てのオブジェクトのプロパティが更新される。

---

### オブジェクト生成時の特徴

---

- オブジェクトの生成時には `constructor` プロパティにアクセスできるようになる（プリミティブ値も同じ）

- `constructor` プロパティの特定は `instanceof` 演算子で判定できる

---

オブジェクトにはネイティブコンストラクタを持つオブジェクトがいくつか存在する。

---

- Object
- Array
- Funciton
- Date
- Error
- RegExp

---

```js

const obj  = new Object();
const arr  = new Array();
const date = new Date();

console.log(obj  instanceof Object);
console.log(arr  instanceof Array);
console.log(date instanceof Date);
// => 全て true が返る

obj.constructor  === Object;
arr.constructor  === Array;
date.constructor === Date;
// => 上記と結果が同じ

```

💡 ネイティブコンストラクタはリテラルでも生成できる。

---

プリミティブ値とネイティブコンストラクタは別物。

配列などはプリミティブ値でないため注意！（意外に知らないで判定を行う人が多い）

`typeof Array` は存在しない 🙅‍♀️🙅‍♀️🙅‍♀️

---

### ☝️

ただ、`instanceof` は `iframe` では**動作しない**ため、
`Array` などの判定は `instanceof` より `Array.isArray()` が推奨されている。

---

### 比較

---

オブジェクト自体の比較は、比較対象のオブジェクトが「同じ型」で「同じ（プロパティの）値」を持っているかどうかで**判断できない。**

```js

const cf_01 = { foo: 'bar' };
const cf_02 = { foo: 'bar' };

cf_01 === cf_02 // => false

const cf_03 = cf_01;

// 参照先が同じものは比較（というか同じなので）できる
cf_03 === cf_01 // => true

```

---

つまりオブジェクトそのものが型も値も同じであるかの判定は別の方法を使用する必要がある。

---

代替法 その1

- [isEqual](https://underscorejs.org/#isEqual)

```js

const stooge = { name: 'moe', luckyNumbers: [13, 27, 34] };
const clone  = { name: 'moe', luckyNumbers: [13, 27, 34] };

stooge === clone;
// => false

_.isEqual(stooge, clone);
// => true

```

---

代替法 その２

- [assert.deepStrictEqual](https://nodejs.org/api/assert.html#assert_assert_deepstrictequal_actual_expected_message)

```js

const stooge = { name: 'moe', luckyNumbers: [13, 27, 34] };
const clone  = { name: 'moe', luckyNumbers: [13, 27, 34] };

assert.deepStrictEqual(stooge, clone);
// => OK

```

---

ビルトインではオブジェクトの比較するためのメソッドや演算子はないため、ライブラリなどを使います。

TypeScript を使用している場合は Lint やコンパイル時に検出できますね。 

---

### まとめ

- 1つ以上のプリミティブ値を格納できるレイヤ
- 複製する場合は参照渡しになる
- プロパティは動的に変更が可能
- 生成されたオブジェクトはコンストラクタプロパティにアクセスができる
  - コンストラクタの判定は `instanceof` で行う
- オブジェクトそのものを比較はできない
  - 別途ライブラリのメソッドなどを使用する

---

### 次回
どうしようかな...