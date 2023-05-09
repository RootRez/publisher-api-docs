## Currencies

You can retrieve currencies supported by the Ripe API via the currencies endpoint

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/currences/.json | GET  |

### Index

> HTTP GET: /publisher/v3.0/currences/.json

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | Your API key  |

Response:

```json
{
    "data": [
        {
            "currency_code": "AUD",
            "name": "Australia",
            "usd_value": 1.42987
        },
        {
            "currency_code": "CAD",
            "name": "Canada",
            "usd_value": 1.309675
        },
        {
            "currency_code": "CHF",
            "name": "Switzerland",
            "usd_value": 0.981625
        },
        {
            "currency_code": "EUR",
            "name": "European Union",
            "usd_value": 0.88115
        },
        {
            "currency_code": "GBP",
            "name": "United Kingdom",
            "usd_value": 0.79076
        },
        {
            "currency_code": "NZD",
            "name": "New Zealand",
            "usd_value": 1.49285
        },
        {
            "currency_code": "USD",
            "name": "United States",
            "usd_value": 1
        }
    ]
}
```
