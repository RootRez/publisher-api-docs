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
        "publisher": {
            "id": 13,
            "name": "My Publisher",
            "google_map_key": "",
            "map_longitude": -111.707555,
            "map_latitude": 40.571296,
            "map_zoom": 12,
            "map_type": "terrain",
            "organization": {
                "id": 3,
                "name": "RootRez",
                "title": "RootRez",
                "currency": "USD",
                "created": "2015-08-18T16:27:52-06:00",
                "modified": null
            },
            "map": {
                "config": {
                    "pins": [
                        {
                            "name": "Local Landmark",
                            "image": "/uploads/Asset-23mtn.png",
                            "description": "Local landmark description",
                            "background_color": "#FFFFFF",
                            "text_color": "#000000",
                            "longitude": -111.629191,
                            "latitude": 40.579011
                        },
                    ]
                },
                "style": [
                    {
                        "elementType": "geometry",
                        "stylers": [
                            {
                                "color": "#e1e1e3"
                            }
                        ]
                    }
                ]
            }
        },
        "organization": "RootRez",
        "organization_currency": "USD",
        "destinations": [
            {
                "id": 33,
                "name": "Alta",
                "country": "US",
                "latitude": 40.588839,
                "longitude": -111.637979,
                "region": "Utah",
                "permalink": "/search/33/us/utah/alta",
                "areas": [
                    {
                        "id": 47,
                        "name": "Town of Alta",
                        "children": []
                    },
                    {
                        "id": 48,
                        "name": "Alta / Snowbird Bypass Road",
                        "children": []
                    },
                    {
                        "id": 49,
                        "name": "Wildcat / Collins Base Area",
                        "children": []
                    },
                    {
                        "id": 40,
                        "name": "Surrounding Area",
                        "children": []
                    },
                    {
                        "id": 209,
                        "name": "Little Cottonwood Canyon",
                        "children": []
                    }
                ],
                "amenities": [
                    {
                        "id": 44,
                        "name": "Shuttle to Slopes"
                    }
                ]
            }
        ]
    }
}
```

