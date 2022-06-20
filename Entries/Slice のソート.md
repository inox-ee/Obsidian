# Slice のソート
#golang 

## 安定性

> 安定ソート（あんていソート、stable sort）とは、ソート（並べ替え）のアルゴリズムのうち、同等なデータのソート前の順序が、ソート後も保存されるものをいう。つまり、ソート途中の各状態において、常に順位の位置関係を保っていることをいう。
> たとえば、学生番号順に整列済みの学生データを、テストの点数順で安定ソートを用いて並べ替えたとき、ソート後のデータにおいて、同じ点数の学生は学生番号順で並ぶようになっている。
> [name=安定ソート - Wikipedia]

## `sort.Slice`

```func Slice(x interface{}, less func(i, j int) bool)```

> [sort package - sort - pkg.go.dev](https://pkg.go.dev/sort#Slice)

安定性の無いソート。

## `sort.SliceStable`

```func SliceStable(x interface{}, less func(i, j int) bool)```

> [sort package - sort - pkg.go.dev](https://pkg.go.dev/sort#SliceStable)

安定性のあるソート。
