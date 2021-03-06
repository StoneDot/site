# BOOST_PP_LIST_REVERSE_D

`BOOST_PP_LIST_REVERSE_D` マクロは 逆順の *リスト* に展開される。
これは `BOOST_PP_WHILE` 内で呼ばれる際には最も効率よく機能する。

## Usage

```cpp
BOOST_PP_LIST_REVERSE_D(d, list)
```

## Arguments

- `d` :
	次の有効な `BOOST_PP_WHILE` 反復。

- `list` :
	逆順にされる *リスト* 。

## See Also

- [`BOOST_PP_LIST_REVERSE`](list_reverse.md)

## Requirements

Header: &lt;boost/preprocessor/list/reverse.hpp&gt;

## Sample Code

```cpp
#include <boost/preprocessor/list/fold_right.hpp>
#include <boost/preprocessor/list/reverse.hpp>

#define L1 (a, (b, (c, (d, BOOST_PP_NIL))))
#define L2 (L1, (L1, (L1, BOOST_PP_NIL)))

#define OP(d, state, x) (BOOST_PP_LIST_REVERSE_D(d, x), state)

BOOST_PP_LIST_FOLD_RIGHT(OP, BOOST_PP_NIL, L2)
/*
	((d, (c, (b, (a, BOOST_PP_NIL)))), ((d, (c, (b, (a, BOOST_PP_NIL)))),
	((d, (c, (b, (a, BOOST_PP_NIL)))), BOOST_PP_NIL)))
	に展開される
*/
```
* BOOST_PP_NIL[link nil.md]
* BOOST_PP_LIST_REVERSE_D[link list_reverse_d.md]
* BOOST_PP_LIST_FOLD_RIGHT[link list_fold_right.md]

