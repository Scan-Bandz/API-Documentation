---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='scanbandz.com/register'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the ScanBandz API
---

# Introduction

Welcome to the ScanBandz API! You can use this API to access and query guest, event, and account information from our database.

We currently offer only examples of language bindings in Shell and Python, but you are free to develop and submit examples in other languages. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Account

## Get Account Details


```python
import requests

response = requests.get('http://localhost:8000/api.v1/account', headers={'Authorization': 'API-KEY'})
print(response.json())

```

```shell
curl "http://scanbandz.com/api.v1/account" \
  -H "Authorization: API-KEY"
```

> Make sure to replace `API-KEY` with your API key.

<aside class="notice">
You must replace <code>API-KEY</code> with your personal API key.
</aside>

> The above command returns JSON structured like this:

```json
{
"Account": {
  "id": 1,
  "username": "admin@scanbandz.com",
  "email": "admin@scanbandz.com",
  "last_login": "2022-09-29T18:15:41.875526-04:00",
  "is_active": true
  },
"User": {
  "full_name": "ScanBandz Admin",
  "phone_number": "",
  "stripe_subscription_id": "",
  "text_updates": true,
  "total_events": 0,
  "total_guests": 0,
  "total_attendance": 0,
  "events_cycle": 0,
  "guests_cycle": 0,
  "attendance_cycle": 0,
  "billing_date": "None",
  "subscription": 1,
  }
}
```

This endpoint retrieves account and billing cycle information.

# Events

## Get Event Details


```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

