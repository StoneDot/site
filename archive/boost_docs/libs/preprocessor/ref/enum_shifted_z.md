# BOOST_PP_ENUM_SHIFTED_z

`BOOST_PP_ENUM_SHIFTED_z` マクロは `BOOST_PP_ENUM_SHIFTED` の繰り返し構築への再入を表す。

## Usage

```cpp
BOOST_PP_ENUM_SHIFTED_ ## z(count, macro, data)
```

## Arguments

- `z` :
	利用可能な次の `BOOST_PP_REPEAT` の次元。

- `count` :
	`macro` を繰り返し呼び出す回数。
	有効な値の範囲は `0` から `BOOST_PP_LIMIT_REPEAT` まで。

- `macro` :
	`macro(z, n, data)` の形の三項演算。
	このマクロは、利用可能な次の反復の深さ、現在の繰り返し番号、付属の `data` の三引数でもって `BOOST_PP_ENUM_SHIFTED` により展開される。

- `data` :
	`macro` に渡される付属データ。

## Remarks

このマクロはコンマ区切りのシーケンスに展開される:

```cpp
macro(z, 1, data), ... macro(z, count - 1, data)
```

プリプロセッサのトークン貼り付け演算子よりも `BOOST_PP_CAT` を用いた連結が必要な場合があるかもしれない。
それは、`z` の値がマクロ呼び出しそのものであるときに起こる。
この場合、マクロの遅延展開が必要となる。
以上のような場合でのシンタックスはこのようになる:

```cpp
BOOST_PP_CAT(BOOST_PP_ENUM_SHIFTED_, z)(count, macro, data).
```

## See Also

- [`BOOST_PP_CAT`](cat.md)
- [`BOOST_PP_ENUM_SHIFTED`](enum_shifted.md)
- [`BOOST_PP_LIMIT_REPEAT`](limit_repeat.md)

## Requirements

Header: &lt;boost/preprocessor/repetition/enum_shifted.hpp&gt;

## Sample Code

```cpp
#include <boost/preprocessor/arithmetic/inc.hpp>
#include <boost/preprocessor/repetition/enum_shifted.hpp>
#include <boost/preprocessor/repetition/repeat.hpp>

#define TEXT(z, n, text) text

#define MACRO(z, n, data) \
	( \
		BOOST_PP_ENUM_SHIFTED_ ## z( \
			BOOST_PP_INC(n), \
			TEXT, data \
			) \
		) \
	/**/

BOOST_PP_REPEAT(3, MACRO, class) // () (class) (class, class) に展開される
```
* BOOST_PP_ENUM_SHIFTED_[link enum_shifted_z.md]
* BOOST_PP_REPEAT[link repeat.md]

