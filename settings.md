## Settings

Retrieves a publishers settings and other meta data such as the destinations associated with the requested publisher. Publisher settings are defined in the [CRS Admin](https://crs.rootrez.com/admin).

Client-side settings are implemented on the client. You may choose to use these settings or ignore them.

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/.json?key=MyKey  | GET  |

Response:

```json
{
    "data": {
        "organization": "Ripe",
        "organization_currency": null,
        "destinations": [
            {
                "id": 27,
                "name": "Boise",
                "country": "US",
                "region": "Idaho",
                "permalink": "/search/27/us/idaho/boise",
                "children": [
                    {
                        "id": 194,
                        "name": "Airport"
                    },
                    {
                        "id": 377,
                        "name": "Downtown"
                    }
                ]
            }
        ],
        "feature_filters": [
            {
                "id": 303,
                "name": "Bike Rentals",
                "icon": "bike-rental"
            }
        ],
        "destinationIDs": [
            0
        ],
        "publisher": {
            "id": 40,
            "name": "Book Westeros (Demo)",
            "map_longitude": -116.190881,
            "map_latitude": 43.613619,
            "map_zoom": 11,
            "map_type": "roadmap",
            "google_map_key": "XYZ",
            "domain": "lodging.bookwesteros.com",
            "organization": {
                "id": 3,
                "name": "Ripe"
            },
            "settings": {
                "client": {
                    "booking_engine": "ota",
                    "sort_type": "manual",
                    "destination_type": "",
                    "title_tag": "",
                    "description_tag": "",
                    "results_per_page": 40,
                    "feature_filter_title": "Features",
                    "google_map_key": "",
                    "publisher_phone": "",
                    "phone_number_call_out": "Talk to a local expert:",
                    "show_hotel_phone": false,
                    "show_external_hotel_link": false,
                    "display_tripadvisor": true,
                    "soldout_text": "Sold Out",
                    "google_analytics": "",
                    "datalayer_ecommerce": false,
                    "additional_terms_and_conditions": "",
                    "booking_disclaimer": "",
                    "currency": "USD",
                    "show_fee_breakdown": true,
                    "promotion_required": false,
                    "minimum_promotion_percent": "",
                    "gdpr_cookie_consent": true,
                    "shopping_cart": false,
                    "shopping_cart_store_id": "",
                    "shopping_cart_token": ""
                },
                "map": {
                    "config": {
                        "pins": [
                            {
                                "name": "Map Pin",
                                "description": "A map pin!",
                                "image": "http://rootrez-media.localhost/map_pins/40/map-pin-1553006655.png",
                                "text_color": "#000000",
                                "background_color": "#FFFFFF",
                                "latitude": 43.610636,
                                "longitude": -116.281862,
                                "zoom_level": 10,
                                "file": "map_pins/40/map-pin-1553006655.png"
                            },
                            {
                                "name": "Another pin",
                                "description": "pins",
                                "image": "http://rootrez-media.localhost/map_pins/40/another-pin-1553611904.png",
                                "text_color": "#000000",
                                "background_color": "#FFFFFF",
                                "latitude": 43.626046,
                                "longitude": -116.184358,
                                "zoom_level": 11,
                                "file": "map_pins/40/another-pin-1553611904.png"
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

### organization

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- |
| organization  | string |  | Name of the publishers parent organization  |
| ~~organization_currency~~  | deprecated |  | Deprecrated  |
| destinations  | array |  | An array of one to many objects describing the destination assigned to the publisher |
| feature_filters  | array |  | An array of one to many objects describing filters associated with the publisher |
| ~~destinationIDs~~  | deprecated |  | Deprecated  |
| publisher  | object |  | An object describing the publisher |

### organization.destination

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- |
| id  | integer |  | Internal identifier of the destination |
| name  | string |  | Name of the destination |
| country  | string |  | Two character country code |
| region  | string |  | Administrative region (state, province etc.) |
| children  | array |  | An array of sub-destination objects |
| permalink  | string |  | A suggested URL for white labels to use |

### organization.feature_filter

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- |
| id  | integer |  | Internal identifier of the filter |
| name  | string |  | Name of the filter |
| icon  | string |  | Icon file to be used to by white label publishers, not applicable to API users |

### organization.publisher

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- 
| id  | integer |  | Internal identifier |
| name  | string |  | Name of publisher |
| map_longitude  | integer |  | Center point on the map for white label publishers |
| map_latitude  | integer |  | Center point on the map for white label publishers |
| map_zoom  | integer | 10 | Map zoom level for white label publishers |
| map_type  | string | roadmap | See Google map types |
| ~~google_map_key~~  | deprecated |  | Deprecated, use organization.publisher.settings.client.google_map_key |
| domain | string |  | The publishers domain |
| settings | object |  | Object describing client and server settings for the publisher |

### organization.publisher.settings.client

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- 
| booking_engine | string | ota | Applicable to Ripe hosted publishers only |
| sort_type | string |  | How properties should be sorted (manual vs random) |
| destination_type | string |  | Controls map display for white label publishers (single vs multiple) |
| title_tag | string |  | HTML title tag for white label publishers |
| description_tag | string |  | HTML title tag for white label publishers |
| results_per_page | integer | 40 | Results to display per page for white label publishers |
| feature_filter_title | string | Features | A custom title for property filtering on white label publishers  |
| google_map_key | string |  | Google map key |
| publisher_phone | string |  | Publisher phone number to display on white labels |
| phone_number_call_out | string |  | Publisher phone number call out text for white labels |
| show_hotel_phone | boolean | false | Whether to show the hotels phone number on white labels (0 or 1) |
| show_external_hotel_link  | boolean | false | Whether to show a link to the hotels website on white labels (0 or 1) |
| display_tripadvisor | boolean | false | Whether to show Trip Advisor Ratings on white labels (0 or 1) |
| soldout_text | string | Sold Out | Messaging to consumer when property is sold out on white labels    |
| google_analytics | string |  | Google analytics UA code for white labels |
| datalayer_ecommerce | boolean | false  | Whether to load Google Tag Manager data layers on white labels  (0 or 1) |
| additional_terms_and_conditions | string |  | Displays additional terms in conditions on white labels checkout page |
| booking_disclaimer | string |  | Adds booking disclaimer to the white labels checkout page |
| currency  | string |  | Three character currency code to display rates in |
| show_fee_breakdown | boolean | true | Whether to display full fee/tax breakdown on white labels checkout page |
| promotion_required | boolean | false | Requires all properties returned to have promotions |
| minimum_promotion_percent | string |  | Used in conjunction with promotion_required |
| gdpr_cookie_consent | boolean | true | Whether to display a GDPR compliant consent message |
| shopping_cart | boolean | false | Applicable only to ski resort publishers |
| shopping_cart_store_id | string |  | Applicable only to ski resort publishers |
| shopping_cart_token | string |  | Applicable only to ski resort publishers |

