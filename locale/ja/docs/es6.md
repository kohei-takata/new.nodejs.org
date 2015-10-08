---
title: ES6
layout: docs.hbs
---
<!--
# ES6 in Node.js
-->

# Node.js における ES6

<!--
Node.js is built against modern versions of [V8](https://developers.google.com/v8/). By keeping up-to-date with the latest releases of this engine, we ensure new features from the [JavaScript ECMA-262 specification](http://www.ecma-international.org/publications/standards/Ecma-262.htm) are brought to Node.js developers in a timely manner, as well as continued performance and stability improvements.
-->

Node.js は新しいバージョンの [V8 エンジン](https://code.google.com/p/v8/) を対象にビルドされています。V8 エンジンを最新版に保つことで、Node.js 開発者は[ECMA-262 specification](http://www.ecma-international.org/publications/standards/Ecma-262.htm)で定義された JavaScript の新機能をすぐに利用することができます。


All ES6 features are split into three groups for **shipping**, **staged**, and **in progress** features:

* All **shipping** features, which V8 considers stable, are turned **on by default on Node.js** and do **NOT** require any kind of runtime flag.
* **Staged** features, which are almost-completed features that are not considered stable by the V8 team, require a runtime flag: `--es_staging` (or its synonym, `--harmony`).
* **In progress** features can be activated individually by their respective harmony flag (e.g. `--harmony_destructuring`), although this is highly discouraged unless for testing purposes.

<!--
## Which ES6 features ship with Node.js by default (no runtime flag required)?
-->

## Node.js でデフォルトで利用可能な ES6 の新機能

* Block scoping (strict mode only)

    * [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

    * [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

    * `function`-in-blocks

    > V8 3.31.74.1時点で、block-scoped declarations は[意図的にstrict modeのコードにしか適用されないように実装されています](https://groups.google.com/forum/#!topic/v8-users/3UXNCkAU8Es)。V8 が ES6 の仕様に追従することで今後この実装に変更があるということを覚えておいてください。

<!--
    // markdown-it の問題で順番を入れ替え
    >As of v8 3.31.74.1, block-scoped declarations are [intentionally implemented with a non-compliant limitation to strict mode code](https://groups.google.com/forum/#!topic/v8-users/3UXNCkAU8Es). Developers should be aware that this will change as v8 continues towards ES6 specification compliance.
-->


<!--
* [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) (strict mode only)
-->

* * [クラス](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) (strict mode でのみ使用可。)


* Collections

    * [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

    * [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)

    * [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

    * [WeakSet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)

* [Typed arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays)

* [Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)

* [Binary and Octal literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Numeric_literals)

<!--
* [Object literal extensions](https://github.com/lukehoban/es6features#enhanced-object-literals) (shorthand properties and methods)
-->

* [拡張オブジェクトリテラル](https://github.com/lukehoban/es6features#enhanced-object-literals) (プロパティとメソッドの省略表現)

* [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

<!--
* [New String methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla#Additions_to_the_String_object)
-->

* [新しい String メソッド](https://developer.mozilla.org/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla#Additions_to_the_String_object)

* [Symbols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

* [Template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings)

* [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

<!--
You can view a more detailed list, including a comparison with other engines, on the [compat-table](https://kangax.github.io/compat-table/es6/) project page.
-->

ほかのエンジンとの比較を含むより詳細な一覧が、[compat-table](https://kangax.github.io/compat-table/es6/)プロジェクトのページで閲覧できます。

<!--
## Which ES6 features are behind the --es_staging flag?
-->

## --es_stagingフラグで使えるES6の機能

<!--
* [`Symbol.toStringTag`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) (user-definable results for `Object.prototype.toString`, behind flag `--harmony_tostring`)
-->

*  [`Symbol.toStringTag`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Symbol) (ユーザーが定義可能な `Object.prototype.toString` 。 `--harmony_tostring` でも有効です。)

<!--
## Which ES6 features are in progress?
-->

## 開発段階のES6の機能

<!--
New features are constantly being added to the V8 engine. Generally speaking, expect them to land on a future Node.js release, although timing is unknown.
-->

V8 エンジンには絶えず新機能が追加されています。一般的に、それらの機能は将来的には Node.js でも使えるようになると言えます。ただし、具体的な時期はまだお伝えできません。

<!--
You may list all the *in progress* features available on each Node.js release by grepping through the `--v8-options` argument. Please note that these are incomplete and possibly broken features of V8, so use them at your own risk:
-->

Node.js に `--v8-options` フラグを渡した結果を grep することで、どの *in progress* な機能が利用可能かを一覧表示できます。ただし、それらは未完成で壊れている可能性のある機能であることに注意してください。各自の責任のもとに使用してください。

```bash
node --v8-options | grep "in progress"
```

<!--
## I have my infrastructure set up to leverage the --harmony flag. Should I remove it?
-->

## --harmonyフラグを利用したインフラがあります。フラグを無効にすべきですか？

<!--
The current behaviour of the `--harmony` flag on Node.js is to enable **staged** features only. After all, it is now a synonym of `--es_staging`. As mentioned above, these are completed features that have not been considered stable yet. If you want to play safe, especially on production environments, consider removing this runtime flag until it ships by default on V8 and, consequently, on Node.js. If you keep this enabled, you should be prepared for further Node.js upgrades to break your code if V8 changes their semantics to more closely follow the standard.
-->

現在の Node.js における `--harmony` フラグの挙動は **staged** features のみを有効化するものです。`--harmony` フラグは Node.js においては `--es_staging` フラグと全く同じ作用をします。上述の通り、それらの機能は完成されてはいるものの、まだ安定しているとは言えません。安全を重視すべき場面、特にプロダクション環境であれば、V8 、ひいては Node.js でデフォルトで利用可能になるまでフラグを無効にすることを検討してください。有効化したまま運用するのであれば、V8 の動作が仕様に近づくことでセマンティクスに変更があった場合、Node.js のアップグレード時に使用中のコードが意図通りに動作しなくなる可能性に備えてください。

<!--
## How do I find which version of V8 ships with a particular version of Node.js?
-->

## Node.js がどのバージョンの V8 を使っているか調べるには？

<!--
Node.js provides a simple way to list all dependencies and respective versions that ship with a specific binary through the `process` global object. In case of the V8 engine, type the following in your terminal to retrieve its version:
-->

Node.js は、使用中の Node.js のすべての依存ソフトウェアとそのバージョンを一覧できる簡単な方法を、`process` グローバルオブジェクトを介して提供しています。例えば、V8 エンジンのバージョンを調べるには、ターミナルで以下のコマンドを入力します。

```bash
node -p process.versions.v8
```
