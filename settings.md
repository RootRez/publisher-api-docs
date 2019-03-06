## Settings

Retrieves a publishers settings and other meta data such as the destinations associated 
with the requested publisher.

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/.json?key=MyKey  | GET  |

Response:

```json
{
    "data": {
        "organization": "RootRez",
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
                "name": "RootRez"
            },
            "settings": {
                "client": {
                    "sort_type": "manual",
                    "destination_type": "single",
                    "title_tag": "A Booking Engine of Ice and Fire",
                    "description_tag": "A Booking Engine of Ice and Fire",
                    "results_per_page": "40",
                    "feature_filter_title": "Features",
                    "google_map_key": "XYZ",
                    "publisher_phone": "",
                    "show_hotel_phone": "0",
                    "show_external_hotel_link": "0",
                    "display_tripadvisor": "1",
                    "soldout_text": "Sold Out",
                    "google_analytics": "",
                    "additional_terms_and_conditions": "",
                    "currency": "USD",
                    "show_fee_breakdown": "1",
                    "promotion_required": "0",
                    "minimum_promotion_percent": "",
                    "shopping_cart": "0"
                },
                "server": null,
                "map": []
            }
        }
    }
}
```

