Reservation
HTTP POST: /publisher/v3.0/book/reservation/.json

The reservation method processes the submitted information and returns a confirmation number upon success.

Reservation Attributes:
All required attributes from preview

Attribute	Type	Required	Default	Definition
rooms	array	yes		Array of room objects, see below
guest	obj	yes		See guest object below
payment	obj	yes		See payment object below
Guest Object
Attribute	Type	Required	Default	Definition
first_name	obj	yes		Guest first name
last_name	obj	yes		Guest first name
email	obj	yes		Guest email address
phone	obj	yes		Guest phone number
note	obj	no		An optional note to the hotel
addresses	array	no		Array of objects
Address Object
Attribute	Type	Required	Default	Definition
type	string	yes		Always Billing
line_1	string	yes		Street address
line_2	string	no		Apartment, Suite, etc...
country	string	yes		Two character ISO country code
postal_code	string	yes		Postal code
region	string	* yes		Non-US reservations only. Province, State, or Administrative Region
state	string	* yes		US reservations only
U.S. addresses: the two character state abbreviation is required for state.
Canadian: the two character province abbreviation is required for region.
Australian: the two character state abbreviation is required for region.
Payment Object
Attribute	Type	Required	Default	Definition
cardholder	string	yes		Cardholders name
month	string	yes		Two character month (00-12)
year	int	yes		Four digit year
cvv	string	yes		CVV or CVV2
postal_code	string	yes		Postal code
Room Object
Attribute	Type	Required	Default	Definition
name	string	yes		Name of guest to put the room under
adults	int	yes		Amount of adults
children	int	no	0	Amount of children
bed_type	string	no	0	Required if bed type option was specified
Reservation Request
{
   "key":"MyKey",
   "property_id":"3144",
   "accommodation_id":"123",
   "rate_code":"REZ",
   "checkin":"2019-01-29",
   "checkout":"2019-01-31",
   "rooms":[
      {
         "name":"RootRez",
         "adults":"2",
         "children":"0",
         "bed_type":false
      }
   ],
   "guest":{
      "first_name":"RootRez",
      "last_name":"RootRez",
      "email":"root@rootrez.com",
      "phone":"8019791437",
      "note":"testing again",
      "addresses":[
         {
            "type":"Billing",
            "line_1":"123",
            "city":"Park City",
            "country":"US",
            "postal_code":"84098",
            "region":"",
            "state":"UT"
         }
      ]
   },
   "payment":{
      "cardholder":"Root Rez",
      "number":"4111111111111111",
      "month":"12",
      "year":"2019",
      "cvv":"644",
      "postal_code":"84098"
   },
   "meta_data":{
      "session_id":"v8klth26ft8qotr09bttk1db53",
      "user_agent":"Mozilla\/5.0 (X11; Linux x86_64) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/59.0.3071.104 Safari\/537.36",
      "ip":"127.0.0.1"
   }
}
