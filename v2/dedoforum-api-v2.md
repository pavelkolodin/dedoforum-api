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

Token is a string to identify client. To get your token go to your Simple Communicator user profile and press the button [ahahaha] then copy your token from text field.

Token example: `12345-67890-12345-67890`

# Common fields for all methods

These fields applied to all methods.

| Name | Type | Comment | Optional |
| :---- | :---- | :---- | :---- |
| `api_token` | string | Your token | |
| `language` | string | Language | YES |

# Methods

## `get_forum_list`

Return list of forums.

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

{"api_token" : "1234567890abcdef", "param" : 2, "foo-bar-bazz" : null}
```

### Response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1234
Connection: keep-alive

{"ok" : true}
```
