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

Definitions:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least), 1, and 2 (most) are supported.  |

Request:

```json
{
   "key": "MyApiKey",
   "limit": 1,
   "verbosity": 2,
   "meta_data":{
      "session_id":"1aa1b1671982e8539aeed0fcd2aadc54",
   }
}
```

Response:

```json
{
    "meta_data": {
        "from_cache": false,
        "count": 1
    },
    "data": [
        {
            "id": 3144,
            "name": "Kings Landing (CRS Test)",
            "room_tax": 0,
            "cutoff_days": 0,
            "order": "10001.3144",
            "discount_rebate_type": "customer",
            "url": "",
            "currency": "USD",
            "is_available": false,
            "unavailable_reason": false,
            "main_telephone": null,
            "is_past_cutoff": null,
            "feature": null,
            "verbosity": 2,
            "was_searched": false,
            "source": false,
            "checkin_time": "03:00 pm",
            "checkout_time": "11:00 am",
            "cutoff_time": "03:00 pm",
            "property_type": {
                "id": 9,
                "name": "Hotel"
            },
            "destination": {
                "id": 27,
                "name": "Boise",
                "areas": null
            },
            "property_description": {
                "short_description": "Lorem ipsum dolor sit amet",
                "long_description": "<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>\n",
                "location_short_description": "",
                "location_long_description": "<p>Lorem ipsum dolor sit amet</p>",
                "why_we_like_it": "<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>\n",
                "staff_pick": "",
                "why_we_like_it_list": [
                    "Lorem ipsum dolor sit amet"
                ],
                "what_you_need_to_know": null,
                "location_description_list": null
            },
            "property_accommodation": [],
            "filter": null,
            "amenity": null,
            "property_image": [
                {
                    "alt": "kings landing",
                    "is_hero_image": false,
                    "season": null,
                    "url": "https://media.rootrez.com//property_images/3144/5c474b9c0db2e_opt.jpg",
                    "url_small": "https://media.rootrez.com//property_images/3144/5c474b9c0db2e_small.jpg",
                    "url_medium": "https://media.rootrez.com//property_images/3144/5c474b9c0db2e_medium.jpg",
                    "external_data": null
                }
            ],
            "property_fee": null,
            "property_provider": [],
            "physical_address": {
                "line_1": "3399 Cassia St",
                "line_2": "",
                "city": "Boise ",
                "country": "US",
                "state": null,
                "administrative_division": "ID",
                "postal_code": "83705",
                "longitude": -116.223559,
                "latitude": 43.5970661,
                "region": ""
            },
            "property_rating": {
                "stars": {
                    "name": "Stars",
                    "value": 4,
                    "meta_data": null
                }
            },
            "property_policy": [],
            "rate": {
                "low": {
                    "total": false,
                    "promotion": false,
                    "discount": false
                }
            },
            "permalink": {
                "geo": "property/3144/us/id/boise/kings-landing-crs-test",
                "property": "property/3144/kings-landing-crs-test"
            },
            "payment_types": [
                {
                    "code": "AX",
                    "name": "American Express",
                    "mandatoryDisplayText": null,
                    "processorCountryCode": null
                },
                {
                    "code": "CA",
                    "name": "Master Card",
                    "mandatoryDisplayText": null,
                    "processorCountryCode": null
                },
                {
                    "code": "DS",
                    "name": "Discover Card",
                    "mandatoryDisplayText": null,
                    "processorCountryCode": null
                },
                {
                    "code": "VI",
                    "name": "Visa",
                    "mandatoryDisplayText": null,
                    "processorCountryCode": null
                }
            ],
            "meta_data": null
        }
    ]
}

```

### Availability

> HTTP POST: /publisher/v3.0/properties/availability/.json

Returns property data with the addition of availability. Take care to use a verbosity level 
that makes sense. When verbosity is increased, requests take longer.

######Definitions:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| properties  | string | yes |  | Comma separated list of property IDs  |
| checkin  | string | yes |  | YYYY-MM-DD  |
| checkout  | string | yes |  | YYYY-MM-DD  |
| rooms  | array | yes |  | An array of room objects. [See room definition below](#room-definition)  |
| promotion | string | no |  | Whether to require a promotion, accepts 'required' |
| discount_code | string | no |  | Discount code |
| currency  | string | no |  |  Three letter ISO currency code. If not supplied will default to setting in the CRS Admin |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least), 1, and 2 (most) are supported.  |

######Room Definition

Specify a room object for each room the customer is looking to book. Note, some properties 
cannot support multi-room bookings.

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| adults  | int | yes |  | Amount of adults  |
| children  | int | no | 0 | Amount of children  |


Request:

```json
{
   "key": "MyApiKey",
   "properties":"3144",
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

Response:

```json
{
    "meta_data": {
        "from_cache": false,
        "total": 1,
        "returned": 1
    },
    "data": [
        {
            "id": 3144,
            "name": "Kings Landing (CRS Test)",
            "is_available": false,
            "was_searched": true,
            "main_telephone": null,
            "order": 1,
            "rate": {
                "low": {
                    "total": false,
                    "promotion": false,
                    "discount": false
                }
            },
            "feature": null,
            "permalink": {
                "geo": "property/3144/us/id/boise/kings-landing-crs-test",
                "property": "property/3144/kings-landing-crs-test"
            },
            "property_description": {
                "staff_pick": ""
            },
            "property_accommodation": [],
            "property_policy": [],
            "property_type": {
                "id": 9,
                "name": "Hotel"
            },
            "physical_address": {
                "line_1": "3399 Cassia St",
                "line_2": "",
                "city": "Boise ",
                "country": "US",
                "state": null,
                "administrative_division": "ID",
                "postal_code": "83705",
                "longitude": -116.223559,
                "latitude": 43.5970661,
                "region": ""
            },
            "destination": {
                "id": 27,
                "name": "Boise",
                "areas": null
            },
            "property_rating": {
                "stars": {
                    "name": "Stars",
                    "value": 4,
                    "meta_data": null
                }
            },
            "filter": [],
            "amenity": [],
            "unavailable_reason": false,
            "property_image": [
                {
                    "alt": "kings landing",
                    "is_hero_image": false,
                    "season": null,
                    "url": "https://media.rootrez.com//property_images/3144/5c474b9c0db2e_opt.jpg",
                    "url_small": "https://media.rootrez.com//property_images/3144/5c474b9c0db2e_small.jpg",
                    "url_medium": "https://media.rootrez.com//property_images/3144/5c474b9c0db2e_medium.jpg",
                    "external_data": null
                }
            ]
        }
    ]
}
```