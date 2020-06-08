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

[View property response](https://github.com/rootrezdev/publisher-api-docs/blob/master/samples/property/property-view-verbosity-3.json).
