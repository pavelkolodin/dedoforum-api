
# Dedoforum API v2

## Endpoint format

`https://nosql.ru/forum/api/v2/METHOD_NAME`

## Methods

### Requirements

All methods works via `HTTP` `GET` or `POST` methods and the request body sent as a `JSON` in body of `HTTP` request. Example:

```json
HTTP/1.1 GET /forum/api/v2/get_forum_list
Host: nosql.ru
Content-Length: 100

{"api_token" : "1234567890abcdef", "param" : 1, "foo-bar" : false}
```


### Common fields for all methods

These fields applied to all methods. **bold** field is mandatory, *italic* is optional.

| Name | Type | Comment | Optional |
| :---- | :---- | :---- | :---- |
| `api_token` | string | Your token | |
| `language` | string | Language | YES |

### `get_forum_list`

Return list of forums.

Request params:

| Name | Type | Comment | Optional |
| ---- | ---- | ---- | ---- |
| 

```
