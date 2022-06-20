# Go の構造体
#golang 

## TL;DR

「構造体」と「type」、「メソッド」は別概念

### 構造体の宣言

```go=
type Person struct {
    name string
    age  int
}
```

### 構造体の初期化 代表例

```go=+
var p *Person
p = &Person{name: "Taro", age: 20}
// ここで p は、構造体のポインタ型の変数。
```

## 構造体

言語仕様[^Struct_types] 曰く、名前と型を持ったフィールドと呼ばれるものの集まり。
`struct` という予約語を使って定義できる。

### 文法

```go
// 公式より
StructType    = "struct" "{" { FieldDecl ";" } "}" .
FieldDecl     = (IdentifierList Type | EmbeddedField) [ Tag ] .
EmbeddedField = [ "*" ] TypeName .
Tag           = string_lit .

// ex) string 型の Name フィールドと int 型の Age フィールドを持つ構造体
struct {
    Name string
    Age  int
}

// 変数定義
var person struct {
    Name string
    Age  int
}

// 初期化
var person struct {
    Name string
    Age  int
}{
    Name: "inox",
    Age:  20
}

// 代入
person.Age = 30
```

けど普通構造体に名前つけて型として宣言するよね、って話。

## `type` (型宣言)

言語仕様[^type-declarations] 曰く、識別子である型名を型に結びつけるもの。
`struct` は `type` ありきで説明されることが多いが、**構造体のためだけに用いられるものではない**。

### 文法

型宣言は、「エイリアス宣言」と「型定義」の2種類ある。以下は「型定義」の例

```go
TypeDecl = "type" ( TypeSpec | "(" { TypeSpec ";" } ")" ) .
TypeSpec = identifier Type .  // identifier = 識別子 ≒ 変数名 でいいハズ
Type     = TypeName | TypeLit | "(" Type ")" .  // = 型名もしくは型リテラル
TypeName = identifier | QualifiedIdent .  // = 既に名前のついている型

// ex) Hex と名付けられた int 型
type Hex int
// ex) MyReader と名付けられた op.Reader 型
type MyReader io.Reader
```

## 型宣言した構造体の初期化あれこれ

```go=
// その 1: 宣言後にフィールドに代入
var p1 Person
p1.name = "taro"
p1.age = 20

// その 2: 順番に入れて初期化
p2 := Person{"taro", 20}

// その 3: ちゃんとフィールドを指定して初期化
p3 := Person{name: "taro", age: 20}

// その 4: ポインタ型として初期化
var p4 *Person
p4 = &Person{name: "taro", age: 20}

// その 5: new() で初期化
var p5 *Person
p5 = new(Person)
p5.name = "taro"
// make() はマップ、スライス、チャネルの初期化に使うものなので、構造体には使えない。
```

ちなみに、初期化関数を作るのがお作法らしい

```go=+
func newPerson(name string, age int) *Person {
    p := &Person{name: name, age: age}
    return p
}
var p *Person = newPerson("taro", 20)
```

---

## 参考

- [The Go Programming Language Specification - go.dev](https://go.dev/ref/spec)
- [Goを学びたての人が誤解しがちなtypeと構造体について #golang - Qiita](https://qiita.com/tenntenn/items/45c568d43e950292bc31)

[^Struct_types]: [spec#Struct_types - go.dev](https://go.dev/ref/spec#Struct_types)
[^type-declarations]: [spec#Type_declarations - go.dev](https://go.dev/ref/spec#Type_declarations)
