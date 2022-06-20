# cURL コマンド
#Linux 

## GET

```shell-session
curl http://localhost:3000
```

## GET with query params

```shell-session
curl "http://localhost:3000?hoge=fuga&fizz=buzz"
```

`""` でくくらないとデフォルトシェルの特殊文字として扱われる

## POST

```shell-session
curl -XPOST \
     -H "Content-type: application/json" \
     -d '{"hoge": "fuga", "fizz": "buzz"}' \
     http://localhost:3000
```

## PUT/PATCH/DELETE

```shell-session
curl -X PUT|PATCH|DELETE http://localhost:3000/users/1
```
