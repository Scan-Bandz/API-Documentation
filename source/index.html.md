---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='https://scanbandz.com/settings'>Get API Key</a>

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

API keys are available under account settings.



# Account

## Get Account Details
```python
import requests

response = requests.get('https://scanbandz.com/api.v1/account', headers={'Authorization': 'API-KEY'})
print(response.json())

```

```shell
curl "https://scanbandz.com/api.v1/account" \
  -H "Authorization: API-KEY"
```

> Make sure to replace `API-KEY` with your API key.



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


Get associated account information, including billing cycle, subscription information, and aggregate data.

<aside class="notice">
You must replace <code>API-KEY</code> with your personal API key.
</aside>

### HTTP Request

`GET https://scanbandz.com/api.v1/account`

### Parameters

Parameter | Type | Description
--------- | ----------- | -----------
Authorization | Header | API Key




# Events

## Get Events Details
```python
import requests

response = requests.get('https://scanbandz.com/api.v1/events', headers={'Authorization': 'API-KEY'})
print(response.json())

```

```shell
curl "https://scanbandz.com/api.v1/events" \
  -H "Authorization: API-KEY"
```

> Make sure to replace `API-KEY` with your API key.

> The above command returns JSON structured like this:

```json
{
  "Events": [
    {
      "pk": 2,
      "title": "Lil Wayne Concert",
      "host": 2,
      "description": "Come join us at the Student Union!",
      "event_date": "2022-09-19",
      "event_time": "04:20:00",
      "created_at": "2022-09-19T14:50:44.509346-04:00",
      "expired": false,
      "guests": 2,
      "qr_generated": false,
      "sms_authentication": false,
      "guests_attended": 0,
      "attendance_ratio": 0,
      "uuid": "ea6e369c-cf22-695e-ada2-c00697d6dc69",
      "access_code": "miamieats"
    }
    {
      "pk": 3,
      "title": "Football Game",
      "host": 2,
      "description": "Come support your team!",
      "event_date": "2022-09-25",
      "event_time": "08:20:00",
      "created_at": "2022-06-19T14:50:44.509346-04:00",
      "expired": true,
      "guests": 202,
      "qr_generated": true,
      "sms_authentication": true,
      "guests_attended": 120,
      "attendance_ratio": 5.9,
      "uuid": "da1e369q-cd21-635e-ada2-d00690d6dc69",
      "access_code": "blazeit"
    }
  ]
}
```
Retrieve all associated event information and data.



### HTTP Request

`GET https://scanbandz.com/api.v1/events`

### Parameters

Parameter | Type | Description
--------- | ----------- | -----------
Authorization | Header | API Key



# Guests
## Get Guest Details
```python
import requests

response = requests.get('https://scanbandz.com/api.v1/guests', headers={'Authorization': 'API-KEY', 'Event': 'EVENT-PK'})
print(response.json())

```

```shell
curl "https://scanbandz.com/api.v1/guests" \
  -H "Authorization: API-KEY"
  -H "Event: EVENT-PK"
```

> The above command returns JSON structured like this:

```json
{
  "Event": {
    "pk": 2,
    "title": "Lil Wayne Concert",
    "host": 2,
    "description": "Come join us at the Student Union!",
    "event_date": "2022-09-19",
    "event_time": "04:20:00",
    "created_at": "2022-09-19T14:50:44.509346-04:00",
    "expired": false,
    "guests": 2,
    "qr_generated": false,
    "sms_authentication": false,
    "guests_attended": 0,
    "attendance_ratio": 0,
    "uuid": "ea6e369c-cf22-495e-ada2-c00569d6dc69",
    "access_code": "miamieats"
  },
  "Guests": [
    {
      "name": "Josh Cap",
      "phone_number": "+19802148999",
      "extra_tickets": 0,
      "attended": true,
      "attendance_time": "None",
      "uuid": "021b9750-6512-4cc6-8aec-dab887c5ced9",
      "qr_code": "None"
    },
    {
      "name": "Cam Newton",
      "phone_number": "+19802148991",
      "extra_tickets": 0,
      "attended": false,
      "attendance_time": "None",
      "uuid": "8c1c1d54-108b-42ef-bf2e-a489078ab5ed",
      "qr_code": "None"
    }
  ]
}
```
Get an event's details and guest list.


### HTTP Request

`GET https://scanbandz.com/api.v1/guests`

### Parameters

Parameter | Type | Description
--------- | ----------- | -----------
Authorization | Header | API Key
Event | Header | Event Primary Key

## Post Guest Details

```python
import requests
data = {
  "Guests": [
    ["Guest Name 1", "Guest Phone 1"],
    ["Guest Name 2", "Guest Phone 2"]
  ]
}
response = requests.post('https://scanbandz.com/api.v1/guests', headers={'Authorization': 'API-KEY', 'Event': 'EVENT-PK'}, json=data)
print(response.json())

```

```shell
curl "https://scanbandz.com/api.v1/guests" \
  -H "Authorization: API-KEY"
  -H "Event: EVENT-PK"
  -d "{'Guests':[['Guest Name 1', 'Guest Phone 1'], ['Guest Name 2', 'Guest Phone 2']]}"
```
> The above command returns JSON structured like this:

```json
{
"Success": "2 guests added.",
"Added Guests": [
    {
      "name": "Test Add",
      "phone_number": "+19802108900",
      "extra_tickets": 0,
      "attended": false,
      "attendance_time": "None",
      "uuid": "5e24433e-dd7e-4fc3-abcc-5443ae994b59",
      "qr_code": "None"
    },
    {
      "name": "Test Add 2",
      "phone_number": "+19802148901",
      "extra_tickets": 0,
      "attended": false,
      "attendance_time": "None",
      "uuid": "3f3eb383-b5ba-4787-93de-88f8a3a77dc0",
      "qr_code": "None"
    }
  ]
}
```
### HTTP Request

`POST https://scanbandz.com/api.v1/guests`

### Parameters

Parameter | Type | Description
--------- | ----------- | -----------
Authorization | Header | API Key
Event | Header | Event Primary Key
Guests | Body | Guest(s) information.

