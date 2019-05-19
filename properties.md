## Properties

Two methods are available for displaying properties assigned to a publisher. One for 
viewing property details and another for retrieving availability.

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/properties/view/.json  | POST  |
| /publisher/v3.0/properties/available/.json  | POST  |

### View

> HTTP POST: /publisher/v3.0/properties/view/.json

Returns property data without availability. Take care to use a verbosity level that makes 
sense. When verbosity is increased, requests take longer.

##### View Definitions:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | Your API key  |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least) - 3 (most) are supported.  |

##### View Request:

```json
{
   "key": "MyApiKey",
   "limit": 1,
   "verbosity": 3,
   "meta_data":{
      "session_id":"39s0m0gt4ubo4d7lsr2b1a1pq5",
      "user_agent":"Mozilla\/5.0 (X11; Linux x86_64) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/68.0.3440.106 Safari\/537.36",
      "ip":"127.0.0.1"
   }
}
```

[View property response](samples/property/property-view-verbosity-3.json).

### Availability

> HTTP POST: /publisher/v3.0/properties/availability/.json

Returns property data with the addition of availability. Take care to use a verbosity level 
that makes sense. When verbosity is increased, requests take longer.

##### Availability Attributes:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | Your API key  |
| properties  | string | yes |  | Comma separated list of property IDs  |
| checkin  | string | yes |  | YYYY-MM-DD  |
| checkout  | string | yes |  | YYYY-MM-DD  |
| rooms  | array | yes |  | An array of room objects. [See room definition below](#room-definition)  |
| promotion | string | no | all | Whether to require a promotion, accepts 'required' or 'all'. If set to 'required' properties without promotions will not be returned |
| discount_code | string | no |  | Discount code |
| currency  | string | no |  |  Three letter ISO currency code. If not supplied will default to setting in the CRS Admin |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least) - 3 (most) are supported.  |

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
   "properties":"3144",
   "verbosity": 2,
   "currency":"USD",
   "checkin":"2019-02-17",
   "checkout":"2019-02-19",
   "discount_code":"",
   "promotion":"all",
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

The response structure is an array of property objects, 
see [property response](samples/property/property-available-verbosity-3.json).


##### Definitions

See [Property Detail](property.md) for definitions
