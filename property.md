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
| key  | string | yes |  | Your API key  |
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
| key  | string | yes |  | Your API key  |
| property_id  | int | yes |  | The property ID  |
| checkin  | string | yes |  | YYYY-MM-DD  |
| checkout  | string | yes |  | YYYY-MM-DD  |
| rooms  | array | yes |  | An array of room objects. [See room definition below](#room-definition)  |
| promotion | string | no | all | Whether to require a promotion, accepts 'required' or 'all'. If set to 'required' properties without promotions will not be returned |
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

[See response](samples/property/property-available-verbosity-3.json). 

##### Definitions

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- |
| id  | integer |  | Property identifier |
| name  | string |  | Property name |
| room_tax  | double | 0 | Tax rate |
| cutoff_days  | integer | 0 | Days the property must be booked in advance of check-in date |
| order  | integer |  | Sort order of the property |
| discount_rebate_type  | string | customer | For discount rebates (inquire with implementation coordinator) |
| url | string |  | Website address |
| currency | string |  | Properties currency (three character currency code) |
| is_available | boolean |  | Whether any rooms are available for booking |
| unavailable_reason  | string |  | A reason the property is unavailable |
| main_telephone  | string |  | Property phone number |
| ~~is_past_cutoff  | bool |  | Deprecated~~ |
| verbosity | integer |  | The requested verbosity level |
| was_searched | string |  | For debugging only |
| source | string |  | The inventory source (crs, sabre, expedia, derbysoft, isi, etc...) |
| checkin_time | string |  | Guest check-in time |
| checkout_time | string |  | Guest check-out time |
| cutoff_time | string |  | Time of day when same day bookings are no longer allowed |
| property_type | object |  | Describes the type of property |
| destination |  |  |  |
| property_description | object |  | Object containing textual descriptions of the property |
| property_accommodation | array |  | An array of room objects |
| filter |  |  |  |
| amenity |  |  |  |
| property_image | array  |  | Array of property image objects  |
| property_fee | |  |  |
| property_provider | |  |  |
| physical_address | object |  | Object describing physical address of the property |
| property_rating | object |  | Object describing the rating of the property |
| property_policy | array |  | Array of objects describing the properties various policies |
| rate | object |  | Object describing rate summary for the property |
| permalink | object |  | Used by white labels only |
| payment_types | array |  | Array of accepted payment types |
| meta_data |  |  |  |
