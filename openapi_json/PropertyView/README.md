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

Returns a single property object, see [view response](https://github.com/rootrezdev/publisher-api-docs/blob/master/properties.md#view-response).
