## Discounts

Discounts can be configured via the CRS Admin interface under your Publisher.

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/discounts/all.json | GET  |

### All

> HTTP POST: /publisher/v3.0/discounts/all/.json

Returns all active discount codes that can be applied to the given stay dates.

##### View Attributes:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | Your API key  |
| checkin  | string | yes |  | Check-in date (YYYY-MM-DD) |
| checkout  | string | yes | | Check-out date (YYYY-MM-DD)  |

Response:

```json
{
    "data": [
        {
            "id": 242,
            "category": "value-add",
            "type": "",
            "code": "OFFERCODE",
            "amount": 20,
            "title": "Gift Card",
            "description": "This gift card is redeemable at the gift shop! ",
            "instructions": "Please bring this confirmation email to the ticket window to pick up your gift card.",
            "non_refundable": false,
            "min_subtotal": 500,
            "received_upon": "checkin",
        },
    ]
}
```

##### Definitions

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- |
| id  | integer |  | Internal identifier |
| ~~type~~  | string |  | Not currently supported |
| category  | string |  | Only value-add is currently supported |
| code  | string |  | The discount code |
| amount | float | | The higher valued, value-add, should have a higher number in the amount field. This is used for sorting and applying the best valued discount |
| title  | string |  | Consumer-facing string to describe the discount |
| instructions  | string | | If any special instructions are required for redeeming this discount |
| non_refundable | bool |  | Indicates if this forces reservations using this code to be non-refunable |
| min_subtotal | float |  | Minimum subtotal the reservation must meet for this discount to be applied |
| received_upon | string |  | When the offer is received (checkin or email) |