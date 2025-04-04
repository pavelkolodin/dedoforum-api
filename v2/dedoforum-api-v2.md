# Table of Contents
1. [URL and Endpoint format](#URL)
2. [Requirements](#Requirements)
3. [Token](#Token)
4. [Methods](#Methods)
5. - [get_state](#get_state)
   - [get_user](#get_user)
   - [get_forum_list](#get_forum_list)
6. [Errors](#Errors)
7. [Examples](#Examples)


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
| `token` | string | Your token | |
| `id` | string | Request id. Hex value. Len: 1...16 bytes. Hex latin symbols only [0-9a-FA-F]. Server must return this id in response to a request. This allows client (in theory; implementation may not support this) to send several requests in parallel in single connection and get responses in any order and match them with requests. Also this guarantees server sent not some cached response. Example: `adef8197fefeaaaa`| |
| `language` | string | Language. | YES |

Example:
```json
{
  "token" : "fead8008deadbeef55aa55aa",
  "id" : "7162534FFA",
  "language" : "RU",
  // other parameters for specific method
}
```


# Methods

## `get_state`

Return the current status of this user for the specified forum, such as ban status, permissions, and so on. Use case: user want to create thread and want to know how many time he must wait before it can do so. This is *tactical* parameters of user related to specific forum, not consistent *long-term parameters* stored in profile. These parameters depend on current state of forum, short-term user behaviour or forum load.

Request (+ [Common fields](#common-fields) )
```json
{
  "forum" : "id123"
}
```

Response:
```json
{
  "ok" : true,
  "state" : {
      // State object
      "forum" : "id123",
      "read" : true,
      "write" : true,
      "time-next-thread" : 1761716231,
      "time-ban-remove" : -1
   }
}
```

State object:

| Name | Type | Comment |
| :---- | :---- | :---- |
| forum | string | forum id |
| read | bool | read access to forum `forum` |
| write | bool | write access to forum `forum` |
| time-next-thread | int | timestamp when new thread can be created. Return 0 if user can create thread NOW. |
| time-ban-remove | int | timestamp ban will be removed from this user on forum `forum`; (-1 mean NEVER - example shows banned user) |



## `get_user`

Get profile data for specified user.

Request:
```json
TODO
```

Response:
```json
{
   "ok" : true,
   "user" : {
      "id" : 81,
      "nickname" : "Гарыныч",
      "motto" : "Я встану, ты ляжешь, запомни это! ГОРОД ГЕРОЙ МОСКВА!!!!",
      "city" : "Москва",
      "avatar" : "file-id",
      "time-registered" : 172817234,
      "time-last-seen" : 172817234,
      "time-ban-remove" : 176251623,    // OPTIONAL
   }
}
```

## `get_forum_list`

Return list of forums with properties of each forum.

Request: [Common fields](#common-fields) ONLY

Response:
```json
{
  "ok" : true,
  "forums" : {
    "8" : {
      // Forum object
      "title" : "Форум бровей,
      "description" : "Форум сбора видосов с 60-летними мужиками в метро, которые едут в вагоне и дёргают брови из лица. Вы смотрите, вас это бесит, а он всё дёргает и дёргает, падла!",
      "threads" : 12345,
      "last-message" : 1782716237,
      "last-author-id" : 701,
      "moderators" : [500, 701, 12]
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

# Errors
Server return `false` in `ok` field of responce. Also field `error` contains error code (integer). Optional field `text` contains error message. Example:
```json
{
  "ok" : false,
  "error" : 11,
  "text" : "Too many requests per second"    // OPTIONAL
}
```

# Examples

## `foo bar` method

Request:

```
GET /forum/api/v2/get_fortune_members_callbacks_hehehe HTTP/1.1
Host: nosql.ru
Content-Length: 12345

{"token" : "1234567890abcdef", "id" : "cadecadec7168", "param" : 2, "foo-bar-bazz" : null}
```

Response:

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1234
Connection: keep-alive

{"ok" : true, "value" : "Dinnahu"}
```
