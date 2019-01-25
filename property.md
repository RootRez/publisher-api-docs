## Property

Two methods are available for displaying property details. One for 
viewing property details and another for retrieving availability.

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/property/view/.json  | POST  |
| /publisher/v3.0/property/available/.json  | POST  |

### View

> HTTP POST: /publisher/v3.0/property/view/.json

Returns property data without availability. Take care to use a verbosity level that makes 
sense. When verbosity is increased, requests take longer.

##### View Attributes:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| property_id  | int | yes |  | The property ID |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least), 1, and 2 (most) are supported.  |

##### View Request:

```json
{
   "key": "MyApiKey",
   "property_id": 3144,
   "limit": 1,
   "verbosity": 2,
   "meta_data":{
      "session_id":"1aa1b1671982e8539aeed0fcd2aadc54",
   }
}
```

##### View Response:

Returns a single property object, see [view response](properties.md#view-response).

### Availability

> HTTP POST: /publisher/v3.0/property/availability/.json

Returns property data with the addition of availability. Take care to use a verbosity level 
that makes sense. When verbosity is increased, requests take longer.

##### Availability Attributes:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| property_id  | int | yes |  | The property ID  |
| checkin  | string | yes |  | YYYY-MM-DD  |
| checkout  | string | yes |  | YYYY-MM-DD  |
| rooms  | array | yes |  | An array of room objects. [See room definition below](#room-definition)  |
| promotion | string | no |  | Whether to require a promotion, accepts 'required' |
| discount_code | string | no |  | Discount code |
| currency  | string | no |  |  Three letter ISO currency code. If not supplied will default to setting in the CRS Admin |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least), 1, and 2 (most) are supported.  |

##### Room Object

Specify a room object for each room the customer is looking to book. Note, some properties 
cannot support multi-room bookings.

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| adults  | int | yes |  | Amount of adults  |
| children  | int | no | 0 | Amount of children  |


##### Availability Request:

```json
{
   "key": "MyApiKey",
   "property_id":"3144",
   "verbosity": 2,
   "currency":"USD",
   "checkin":"2019-02-17",
   "checkout":"2019-02-19",
   "discount_code":"",
   "promotion":"",
   "rooms":[
      {
         "adults":2,
         "children":0
      }
   ],
   
   "meta_data":{
      "session_id":"39s0m0gt4ubo4d7lsr2b1a1pq5",
      "user_agent":"Mozilla\/5.0 (X11; Linux x86_64) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/68.0.3440.106 Safari\/537.36",
      "ip":"127.0.0.1"
   }
}
```

##### Availability Response:

The response structure is an array of property objects, see [view response](properties.md#view-response). 
The following additional availability information is returned:

Rate Data:

```json
{
    "rate": {
        "low": {
            "total": {
                "original_nightly_avg": "100",
                "nightly_avg": "100",
                "original_subtotal": "200.00",
                "subtotal": "200.00",
                "tax": "0.00",
                "fee": "0.00",
                "balance_due": "0.00",
                "checkin_fee": "0.00",
                "total": "200.00",
                "rebate": 0,
                "promotional_savings": "0.00",
                "discount_savings": 0
            },
            "promotion": false,
            "discount": false
        }
    }
}
```

```json
{
    "rate": {
        "low": {
            "total": {
                "original_nightly_avg": "100",
                "nightly_avg": "100",
                "original_subtotal": "200.00",
                "subtotal": "200.00",
                "tax": "0.00",
                "fee": "0.00",
                "balance_due": "0.00",
                "checkin_fee": "0.00",
                "total": "200.00",
                "rebate": 0,
                "promotional_savings": "0.00",
                "discount_savings": 0
            },
            "promotion": false,
            "discount": false
        }
    }
}
```