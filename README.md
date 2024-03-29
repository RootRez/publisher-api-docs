# Ripe API Reference

## API documentation for Ripe products and services. 


 This will help guide you through the process of connecting to our API. The Ripe (formally RootRez) operates as a gateway for registered clients and partners to view properties, book reservations, and retrieve other meta data. The API is a restful-like web service that can be accessed via JSON payloads over HTTPS GET or POST depending on the endpoint. Before getting started, take a moment to familiarize yourself with some [definitions](https://github.com/rootrezdev/publisher-api-docs/wiki/Definitions) pertinent to this implementation.


Typical application workflow ([see example site](https://lodging.bookwesteros.com)):

[Load Settings](settings.md) Load any pertinent settings into your local cache.

[Get Properties](properties.md) Best practice is to request all properties via a verbose call to properties/view.json storing the static property meta data in a local cache. Then update lead rates with low-verbosity calls to properties/available.json. XHR calls can be used within your client to load full room rates with singular calls to property/available.json

[Property Detail](property.md) Typically used for XHR calls to get additional property data from your search results page or when browsing direct to a property page.

[Checkout Preview](book.md#preview) The preview call will perform a real-time inventory lookup where possible. This should only be called on your checkout page implementation.


[Book Reservation](book.md#book) For booking a reservation only.

[View Reservation](reservation.md) Will return single or multiple reservations.

## Misc

[Discounts](discounts.md) Retrieve discount code information.

## Getting Starting

If you haven't already, [contact Ripe](https://www.bookripe.com) to get started. Your technical implementation coordinator will email you the following details:

- API key
- Sandbox environment details
- [Postman](https://www.getpostman.com/) request/response collections

## Hello World 

Say hello world with us.

|  Endpoint | /publisher/v3.0/.json?key=MyKey |
| ------------- | ------------- |
| HTTP  | GET  |


Response:

```json
{
    "uptime": "4 days 23:37:42.78",
    "message": "Thanks for saying hello. Everything looks good so far."
}
```

## HTTP POST Requirements

When doing HTTP POST requests to the API the following meta data fields are required: 
 * session_id: The browsers session identifier
 * user_agent: The browser user agent string
 * ip: The end-users IP Address

```json
{
   "key": "MyAPIKey",
   "meta_data":{
      "session_id":"1aa1b1671982e8539aeed0fcd2aadc54",
      "user_agent":"Mozilla\/5.0 (X11; Linux x86_64) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/63.0.3239.132 Safari\/537.36",
      "ip":"127.0.0.1"
   }
}
```

## Best Practices

* Use HTTPS. All communication with Ripe is handled over HTTPS.
* Keep your API key out of version control (such as GIT or SVN), instead store in a local config file or similar secure means.
* Cache data that is unlikely to change frequently such as property data (not including rates) and client settings.
* Use low verbosity levels (0 is lowest, 3 is highest). The less data requested, the faster 
the response.
* Pre-validate customer data such as billing address, email address, and credit card data before making requests to Ripe. While we do validate this information, creating client-side checks for your customers can greatly improve the booking experience.
* It's advised that you watch this project so you receive notices on changes to documenation, which may include new additions to the API.

## Development Life Cycle

1. Read the documentation.
2. Develop your client
3. Notify your implementation coordinator of completion to receive certification steps.
4. Complete certification process and be granted production access.
5. Complete test booking in production.

## HTTP Status Codes

HTTP Status Codes are used to provide errors, these will be accompanied by error messages. 
Successful requests will result in a 200 OK code. 

|  Attribute | Type | Definition |
| ------------- | ------------- | ------------- |
| type  | string | Exception name |
| message | string |  A description of the error |
| url  | string |  The requested URI |
| code  | int |  HTTP status code |

Example:

```json
{
    "type": "BadRequestException",
    "message": "Unable to parse JSON. Is the request body malformed?",
    "url": "/publisher/v3.0/property/available.json",
    "code": 400
}
```

**400 BadRequestException**

Your request is likely missing required information or json is malformed.

**401 UnauthorizedException**

Authentication failed, you probably have an invalid key or a key has not been setup.

**404 NotFoundException**

Resource or hotel property does not exist, or cannot be returned due to business logic.

**5xx InternalServerErrorException**

This and a 500 Exception, are general exception messages. Most 500 level responses should be one of the types below.

## Specific Exceptions

Most exceptions will be accompanied with additional data in the message string. These can be caught in your application and specific, user-friendly messages can be created for your end-users.

**RoomUnavailableException**

The requested room is not available for booking.

**BookingValidationException**

Invalid data was received in your booking request

**AddressValidationException**

Any address related errors on a booking request.

**CreditCardException**

Invalid credit card data. Either we couldn’t verify the cardholders account or it failed a Luhn algorithm check. 
You should pre-check credit cards against the Luhn algorithm in your implementation.

**RemoteInventoryException**

Ripe was unable to verify the inventory exists in the hotels inventory system or within a third-parties inventory system.

**RemoteInformationException**

Ripe was unable to retrieve hotel meta data from the hotels information system and/or 
third party system.

**DuplicateBookingException**

A similar booking has already been processed.
