### Availability

> HTTP POST: /publisher/v3.0/property/available/.json

Returns property data with the addition of availability. Take care to use a verbosity level 
that makes sense. When verbosity is increased, requests take longer.

##### Availability Attributes:

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| key  | string | yes |  | Your API key  |
| property_id  | int | yes |  | The property ID  |
| checkin  | string | yes |  | YYYY-MM-DD  |
| checkout  | string | yes |  | YYYY-MM-DD  |
| rooms  | array | yes |  | An array of room objects. [See room definition below](#room-definition)  |
| promotion | string | no | all | Whether to require a promotion, accepts 'required' or 'all'. If set to 'required' properties without promotions will not be returned |
| discount_code | string | no |  | Discount code |
| currency  | string | no |  |  Three letter ISO currency code. If not supplied will default to setting in the CRS Admin |
| limit  | int | no | 0 | Limits the number of results returned. 0 will return all  |
| verbosity | int | no  | 0 | Controls the amount of data returned. 0 (least), 1, and 2 (most) are supported.  |

##### Room Object

Specify a room object for each room the customer is looking to book. Note, some properties 
cannot support multi-room bookings.

| Attribute | Type | Required | Default | Definition |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| adults  | int | yes |  | Amount of adults  |
| children  | int | no | 0 | Amount of children  |


##### Availability Request:

```json
{
   "key": "MyApiKey",
   "property_id":"3144",
   "verbosity": 2,
   "currency":"USD",
   "checkin":"2019-02-17",
   "checkout":"2019-02-19",
   "discount_code":"",
   "promotion":"all",
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

##### Availability Response:

[See response](samples/property/property-available-verbosity-3.json). 

##### Definitions

| Attribute | Type | Default | Definition |
| ------------- | ------------- | ------------- | ------------- |
| id  | integer |  | Property identifier |
| name  | string |  | Property name |
| room_tax  | double | 0 | Tax rate |
| cutoff_days  | integer | 0 | Days the property must be booked in advance of check-in date |
| order  | integer |  | Sort order of the property |
| discount_rebate_type  | string | customer | For discount rebates (inquire with implementation coordinator) |
| url | string |  | Website address |
| currency | string |  | Properties currency (three character currency code) |
| is_available | boolean |  | Whether any rooms are available for booking |
| unavailable_reason  | string |  | A reason the property is unavailable |
| main_telephone  | string |  | Property phone number |
| ~~is_past_cutoff~~  | deprecated |  | Deprecated |
| verbosity | integer |  | The requested verbosity level |
| was_searched | boolean |  | Lets the client know whether an ARI search was performed on the property |
| source | string |  | The inventory source (crs, sabre, expedia, derbysoft, isi, etc...) |
| checkin_time | string |  | Guest check-in time |
| checkout_time | string |  | Guest check-out time |
| cutoff_time | string |  | Time of day when same day bookings are no longer allowed |
| property_type | object |  | Describes the type of property |
| destination |  |  |  |
| property_description | object |  | Object containing textual descriptions of the property |
| property_accommodation | array |  | An array of room objects |
| filter | array |  | An array of filter objects |
| amenity | array |  | An array of amenity objects  |
| property_image | array  |  | Array of property image objects  |
| property_fee | array |  | An array of objects describing property fees |
| property_provider | array |  | An array of objects describing this properties available inventory connections |
| physical_address | object |  | Object describing physical address of the property |
| property_rating | object |  | Object describing the rating of the property |
| property_policy | array |  | Array of objects describing the properties various policies |
| rate | object |  | Object describing rate summary for the property |
| permalink | object |  | Used by white labels only |
| payment_types | array |  | Array of accepted payment types |
| is_tripadvisor_partner | bool | false | If this setting is enabled, enhanced trip advisor reviews will be available |
| book_direct_link | string | | Only applicable to RootRez hosted booking engines | 
| reviews | array | | Trip Advisor review data will be returned if possible. [Non partner review sample](samples/tripadvisor/tripadvisor-free-reviews.json) vs [Partner review sample](samples/tripadvisor/tripadvisor-partner-reviews.json) |
| tripadvisor_location | object | | Trip Advisor location data will be returned if possible. [See sample](samples/tripadvisor/tripadvisor-location-data.json) |
| meta_data |  |  |  |

##### property.property_accommodation

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| id | integer |  | Room identifier  |
| name | string |  | Name of the room |
| standard_occupancy | integer |  | Standard occupancy of the room (amount of guests) |
| maximum_occupancy | integer |  | Maximum number of guests allowed |
| short_description | string | | A brief description of the room |
| long_description | string | | A longer description of the room |
| bedding | string | | A description of the bedding types available |
| type | string | | Type of room |
| ~~adult_maximum_occupancy~~ | deprecated | |  |
| ~~child_maximum_occupancy~~ | deprecated | |  |
| ~~adult_rate_adjustment~~ | deprecated | |  |
| ~~child_rate_adjustment~~ | deprecated | |  |
| is_available | boolean | | Whether the room is available for booking |
| is_closedout | boolean | | Whether the room is closed out for booking |
| is_occupancy_exceeded | boolean | | Whether the requested guest amounts exceed occupancy |
| has_no_inventory | boolean | | Whether the room has no inventory |
| is_less_than_min_stay | boolean | | Whether the requested dates are less than minimum stay required |
| is_greater_than_max_stay | boolean | | Whether the requested dates are greater than maximum stay allowed |
| ~~unavailable_reason~~ | deprecated | |  |
| ~~property_accommodation_type~~ | deprecated | |  |
| rates | array | | An array of rate objects |

##### property.property_accommodation.rate

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| code | string |  | Rate code identifier  |
| description | object |  | An object that describes the rate |
| balance_due | double |  | The balance due at time of booking |
| is_refundable | string |  | Whether the rate is refundable (can be Y (yes), N (no), or empty for unknown (see property_policy) |
| is_deposit_required | string |  | Whether a deposit is required (can be Y (yes), N (no), or empty for unknown (see property_policy) |
| deposit_policy | string |  | Rate level deposit policy, takes precedence over other property policies. Not all rates return a deposit policy. |
| cancellation_policy | string |  | Rate level cancellation policy, takes precedence over other property policies. Not all rates return a deposit policy. |
| total | object |  | An object describing the total costs of this rate |
| beds | array |  | An array of bedding objects, if not empty, users must be presented with list of bedding options at time of booking |
| tax_items | array |  | Only populated when calling book/preview |
| fees | array |  | Only populated when calling book/preview |
| checkin_fees | array |  | Only populated when calling book/preview |
| promotion | object |  | The primary promotion applied |
| nights | array |  | An array of night objects describing each nights rates within the requested stay range |
| property_accommodation_image | array |  | An array of image objects |
| discount | object |  | The applied discount code |
| ~~message~~ | deprecated |  |  |
| ~~meta_data~~ | deprecated |  |  |
| ~~tmp~~ | deprecated |  |  |
| promotions | array |  | An array of promotion objects applied |

##### property.property_accommodation.rate.total

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| original_nightly_avg | double |  | Average nightly average before discounts are applied |
| nightly_avg | double |  | The nightly average of the rate |
| original_subtotal | double |  | Subtotal prior to discounts being applied |
| subtotal | double |  | Subtotal amount |
| tax | double |  | Total taxes  |
| fee | double |  | Total fees |
| balance_due | double |  | Total balance due at time of booking |
| checkin_fee | double |  | Additional fees due at time of check-in (not included in balance due or total) |
| total | double |  | Total booking amount |
| rebate | double |  | Customer rebate amount if any |
| promotional_savings | double |  | Amount of promotional savings applied |
| discount_savings | double |  | Amount of discount savings applied |
| ~~group~~ | deprecated | | Deprecated |

##### property.property_accommodation.rate.night

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| rate | double |  | Rate |
| ~~minimum~~ | deprecated |  |  |
| ~~maximum~~ | deprecated |  |  |
| original_rate | double |  | Rate before promotions were applied |
| promotional_savings | double |  | Amount of promotional savings applied |
| promotional_id | int |  | The ID of the applied promotion |
| inventory | int |  | Inventory available (only certain inventory sources will provide inventory counts, no inventory counts available on free sales) |
| date | string |  | Date |

##### property.property_accommodation.rate.promotion

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| id | integer |  | Identifier |
| display_string | string |  | Shortened version of the promotion |
| name | double |  | Full name of the promotion |
| promotion_type_id | int |  | Promotion type identifier |
| amount | double |  | Amount of promotion |
| discount_applied | double |  | Total promotion applied to rate |
| total_discount | double |  | Total promotion applied to rate |
| promotion_type | object |  | Object describing the type of promotion |

##### property.property_accommodation.rate.discount

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| id | integer |  | Identifier |
| category | string |  | Categories are value-add, promotion, and discount |
| type | |  |  |
| code | string |  | The discounts code (supplied in request) |
| amount | double |  | The amount (not applicable for value-adds) |
| description | string |  | Description of the discount |
| instructions | string |  | Instructions to be provided to the guest (only applicable for value-adds) |
| non_refundable | boolean |  | If true, the rate is not refundable when the discount is applied |
| min_subtotal | double |  | Minimum required sub-total for the discount to be applied |
| display_string | string |  | Same as description |
| received_upon | string |  | Can be check-in or email (only applicable to value-adds) |
| discount_applied | double |  | The total discount applied |
| rebate_applied | string |  | Only applicable to category of discount |
| rebate_type | string | customer | Only applicable to category of discount  |

##### property.property_accommodation.property_accommodation_image

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| alt | string |  | HTML Alt attribute text |
| ~~is_hero_image~~ | deprecated |  |  |
| ~~season~~ | |  | deprecated |
| url | string |  | Full image |
| ~~url_small~~ | double |  | Deprecated |
| ~~url_medium~~ | string |  | Deprecated |
| ~~external_data~~ |  |  | Deprecated |

> Note, image URLs will display full-sized images. You can reduce the size and thus load on your end-users browsers with the width and height parameters. Example: https://img.rootrez.com/property_images/3144/kings-landing-crs-test-317fb9ea1d18a46ad0e96bb399224bbe.jpg?width=300&height=200

##### property.filter

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| id | integer |  | ID of the filter relating to the publishers filters |
| name | string |  | Name of the filter |

##### property.amenity

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| id | integer |  | ID of the amenity |
| name | string |  | Name of the amenity |
| category | string |  | Parent category of the amenity |
| ~~group~~ | deprecated | | Deprecated |

##### property.property_image

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| alt | string |  | HTML Alt attribute text |
| ~~is_hero_image~~ | deprecated |  |  |
| season | string |  | Can be empty, summer, or winter |
| url | string |  | Full image |
| ~~url_small~~ | double |  | Deprecated |
| ~~url_medium~~ | string |  | Deprecated |
| ~~external_data~~ |  |  | Deprecated |

> Note, image URLs will display full-sized images. You can reduce the size and thus load on your end-users browsers with the width and height parameters. Example: https://img.rootrez.com/property_images/3144/kings-landing-crs-test-317fb9ea1d18a46ad0e96bb399224bbe.jpg?width=300&height=200

##### property.property_fee

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| type | string |  | Informs whether the fee is a flat fee (dollar) or percentage  |
| applied | string |  | Informs whether the fee is applied once or for each night |
| description | string |  | Description of the fee |
| fee | double |  | The fee amount (see type to know if the fee is a dollar amount or percentage) |
| is_taxable | bool | false | Whether the fee is taxable |
| tax_rate | double | 0 | Applicable if is_taxable is set to true |

##### property.property_provider

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| id | integer |  | Internal ID  |
| name | string |  | Name of the connection |

##### property.physical_address

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| line_1 | string |  | Street address  |
| line_2 | string |  | Suite |
| city | string |  | City |
| country | string |  | Two character country code |
| administrative_division | string | | State, province, or other administrative region |
| postal_code | string |  | Mail service code |
| longitude | integer | | Longitude |
| latitude | integer | | Latitude |
| ~~region~~ | deprecated | | Deprecated |
| ~~state~~ | deprecated | | Deprecated |

##### property.property_policy

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| name | string |  | name of policy  |
| description | string |  | description of policy |

##### property.payment_type

| Attribute | Type | Default | Definition | 
| ------------- | ------------- | ------------- | ------------- |
| code | string |  | Two character credit card code  |
| name | string |  | Credit Card company |
| mandatoryDisplayText | string |  | If set, this string must be displayed to the customer on the checkout page  |
| processorCountryCode | string |  | Where the payment will be processed, required in some countries |