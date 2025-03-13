# prism-anyof-single-array

Demo of possible bug in stoplight/prism. <https://github.com/stoplightio/prism/issues/2675>

## Single element query

```sh
curl 'localhost:4011/users?id=1
```

```json
{"type":"https://stoplight.io/prism/errors#UNPROCESSABLE_ENTITY","title":"Invalid request","status":422,"detail":"Your request is not valid and no HTTP validation response was found in the spec, so Prism is generating this error for you.","validation":[{"location":["query","id"],"severity":"Error","code":"type","message":"Request query parameter id must be array"},{"location":["query","id"],"severity":"Error","code":"anyOf","message":"Request query parameter id must match a schema in anyOf"}]}%
```

## Querying multiple ids

```sh
curl 'localhost:4011/users?id=1&id=2
```

Works as expected

```json
{"users":[{"id":"1","email":"test1@example.com","locale":"en"}]}%
```

## Workarounds

Without `anyOf` this seems to work fine. Below query also works

```sh
curl 'localhost:4011/users?id[]=1
```
