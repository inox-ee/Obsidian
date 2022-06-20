# `mv` コマンド
#shell #Linux

## Case 1
### TL;DR
wildcard と併用する際は、必ず DEST を指定せよ。

### 内容
`mv` コマンドと `*` (wildcard) はよく併用される(`git clone` 等で、宛先ディレクトリを指定せずにネストしてしまった時など)。
```shell
$ mv hoge/* ./
```

シェルとしては、以下のように  `*` が展開され実行されている。
```shell
$ mv hoge/file1 hoge/file2 ./
```

この時、末尾の DEST を忘れるとどうなるか。正解は **file2 が上書きされる** (以下の例では `mv` は `mv -i` にエイリアスされている)。
```shell
$ mv test1.txt test2.txt
mv: overwrite 'test2.txt'? n
```

そもそも、`mv` コマンドは移動ではなく、リネームが主目的とされている。
> Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY. (by `man mv`)

実際に、第2引数としてディレクトリを指定した場合、シェルの解釈としては以下の通りである
。
```shell
$ mv file1 dir1
=
$ mv file1 dir1/file1
```

結論、不用意な上書きを防ぐために `-i,--interactive` / `-b,--backup` オプションを使おう。
