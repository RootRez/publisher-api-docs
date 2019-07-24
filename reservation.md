## Reservations

Two methods are available for retrieving existing reservations.

| Endpoint | HTTP |
| ------------- | ------------- |
| /publisher/v3.0/reservation/view/.json  | GET  |
| /publisher/v3.0/reservation/index/.json  | GET  |


### View

Retrieves a single reservation

> HTTP GET: /publisher/v3.0/reservation/.json

##### Parameter Definitions:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | The API Key |
| id  | int | no |  | The reservation ID  |
| reservation_number  | string | no |  | The reservation IDX string  |


[See response](samples/reservation/view.json). 

### Index

Retrieves many reservations

> HTTP GET: /publisher/v3.0/reservation/index.json

##### Parameter Definitions:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | The API Key |
| checkin  | string | no |  | YYYY-MM-DD The check-in date (must be paired with checkout) |
| checkout  | string | no |  | YYYY-MM-DD The check-out date (must be paired with checkin) |
| created_start  | string | no |  | YYYY-MM-DD The date the booking was created (must be paired with created_end) |
| created_end  | string | no |  | YYYY-MM-DD The date the booking was created (must be paired with created_start) |
| discount  | string | no |  | Discount code used on the booking |
| limit  | int | no | 100 | Limits the result set |
| page  | int | no | 1 | For paging through results |

The response will be an array of objects. [See response](samples/reservation/view.json). 
