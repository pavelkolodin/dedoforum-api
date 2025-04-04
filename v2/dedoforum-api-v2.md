# Table of Contents
1. [URL and Endpoint format](#URL)
2. [Requirements](#Requirements)
3. [Token](#Token)
4. [Methods](#Methods)
5. [Examples](#Examples)


# URL

API endpoint format is following:

https://nosql.ru/forum/api/v2/METHOD_NAME

# Requirements

All methods works via `HTTP` `GET` or `POST` methods and the request body sent as a `JSON` in body of `HTTP` request. See examples section at the end of document.

# Token

Token is a string to authorize the client. To get your token go to your Simple Communicator user profile and press the button [PIDOR AHAHA] then copy your token from text field.

Token example: `12345-67890-12345-67890`

**WARNING!!!! TODO for Deda**: replace this dashed numbers with some hex or string value like `sha256(something)`, example: `703cfa2585a735f8213a886546b7120a02ca3564d6a98d4d3469d35f5b88ad75`. Current API token is too weak and short!

Example Telegram token format: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11` -- larger than 128 bits!

# Common fields

These fields must present in all requests

| Name | Type | Comment | Optional |
| :---- | :---- | :---- | :---- |
| `api_token` | string | Your token | |
| `id` | string | Request id. Hex value. Len: 1...16 bytes. Hex latin symbols only [0-9a-FA-F]. Server must return this id in response to a request. This allows client (in theory; implementation may not support this) to send several requests in parallel in single connection and get responses in any order and match them with requests. Also this guarantees server sent not some cached response. Example: `adef8197fefeaaaa`| |
| `language` | string | Language. | YES |

# Methods

## `get_forum_list`

Return list of forums with properties of each forum.

Request:
```json
// use common parameters
{}
```
Response:
```
{
  "ok" : true,
  "forums" : {
    "8" : {
      // Forum object
      "title" : "Форум рулеза и турбования",
      "description" : "Форум рулеза, трубования, кочевглыжества и цуфлепропермахерства с оттенком волынских пучеров",
      "threads" : 12345,
      "last-message" : 1782716237
    }
  }
}
```

Forum object:
| Name | Type | Comment |
| :---- | :---- | :---- |
| title | string | Forum title |
| description | string | Forum description |
| threads | int | Number of threads in this forum |
| last message | int | Timestamp of last message |





## `get_topic_list`

## `get_post_list`

## `get_post`

## `get_user_data`

## `get_attachment`

## `post_message`

## `update_message`

## `post_attachment`

## `delete_posts`

## `restore_posts`

# Examples
Some examples here.

## Method Foo Bar

### Request

```
GET /forum/api/v2/get_fortune_members_callbacks_hehehe HTTP/1.1
Host: nosql.ru
Content-Length: 12345

{"api_token" : "1234567890abcdef", "id" : "cadecadec7168", "param" : 2, "foo-bar-bazz" : null}
```

### Response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1234
Connection: keep-alive

{"ok" : true}
```
