## Booking

Two methods are made available for bookings: preview and reservation. 

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/book/preview/.json  | POST  |
| /publisher/v3.0/book/reservation/.json  | POST  |

### Preview

> HTTP POST: /publisher/v3.0/book/preview/.json

The preview method is for use on pre-checkout pages to display nightly rates, discounts, 
subtotal, taxes, fees, and totals. 

##### Preview Attributes:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | Your API key  |
| property_id  | int | yes |  | The property ID |
| accommodation_id  | int | yes |  | The room ID  |
| rate_code | string | yes  |  | The rate plan for the room  |
| checkin  | string | yes |  | YYYY-MM-DD  |
| checkout  | string | yes |  | YYYY-MM-DD  |
| rooms  | array | yes |  | An array of room objects. [See room definition](property.md#room-definition)  |
| discount_code | string | no |  | Discount code |
| currency  | string | no |  |  Three letter ISO currency code. If not supplied will default to setting in the CRS Admin |


```json
{
   "key":"MyKey",
   "property_id":"3144",
   "accommodation_id":"123",
   "rate_code":"REZ",
   "checkin":"2019-01-29",
   "checkout":"2019-01-31",
   "discount_code": "",
   "rooms":[  
      {  
         "adults":2,
         "children":0
      }
   ],
   "meta_data":{
      "session_id":"1aa1b1671982e8539aeed0fcd2aadc54",
      "user_agent":"Mozilla\/5.0 (X11; Linux x86_64) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/63.0.3239.132 Safari\/537.36",
      "ip":"127.0.0.1",
   }
}
```

##### Preview Response:

The preview response is similar to a property/available.json response, but contains a complete 
breakdown of taxes and fees. [See full response](https://github.com/rootrezdev/publisher-api-docs/blob/master/samples/book/preview.json).
