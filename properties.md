## Properties

Two methods are available for displaying properties assigned to a publisher. One for 
viewing property details and another for retrieving availability.

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/properties/view/.json  | POST  |
| /publisher/v3.0/properties/available/.json  | POST  |

### View

Returns property data without availability. Take care to use a verbosity level that makes 
sense. When verbosity is increased, requests take longer.

Request:

```json
{
   "key": "MyApiKey",
   "limit": 0,
   "verbosity": 0,
   "meta_data":{
      "session_id":"1aa1b1671982e8539aeed0fcd2aadc54",
   }
}
```

Definitions:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least), 1, and 2 (most) are supported.  |

