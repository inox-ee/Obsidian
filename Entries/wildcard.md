# `*` (wildcard)の挙動について
#Linux #shell 

## TL;DR
`*` は hidden files を含めない。
zsh の場合 `*(D)` とすることで全てのファイル(及びディレクトリ)を展開可能。

## 仕様
重要な仕様として、 `*` はシェルで展開される。

## 挙動
例として、以下のディレクトリを考える。
```
.
└── hoge/
    ├── .test5
    ├── .test6
    ├── test1.txt
    ├── test2.txt
    ├── test3
    └── test4
```

この時、`hoge/` 下では
```shell
$ echo *
fuga test1.txt test2.txt test3 test4
$ echo *.*
test1.txt test2.txt
$ echo *(D)
.test5 .test6 fuga test1.txt test2.txt test3 test4
```
となる。

## 補足
- [[mv command]] で注意。