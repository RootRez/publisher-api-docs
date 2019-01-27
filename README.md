# RootRez Publisher API Documentation

This document is meant to guide a developer through the process of connecting to the (RootRez API)[https://www.rootrez.com/support/developers/]. 
The Publisher API operates as a gateway for registered publishers to view properties, book 
reservations, and retrieve other meta data you’d except from an Online Travel Agency (OTA). 
The API is a restful-like web service that can be accessed via JSON payloads over HTTPS GET or
 POST depending on the endpoint. Before getting started, take a moment to familiarize yourself with 
 some [definitions](https://github.com/rootrezdev/publisher-api-docs/wiki/Definitions) pertitent to this implementation.

Typical application workflow:

1. [Load Settings](settings.md)
2. [Get Properties](properties.md)
3. [Property Detail](property.md)
4. [Checkout Preview](book.md#preview)
5. [Book Reservation](book.md#book)
6. [View Reservation](reservation.md)

## Environments

Prior to being given a production key your application will need to be certified by the 
RootRez development team in our sandbox environment. 

**Sandbox** 

https://api-sandbox.rootrez.com/publisher/v3.0/

**Production** 

https://svc.rootrez.com/publisher/v3.0/

## Authentication

Access can be obtained through the use of a Publisher Key. This key will be provided by 
your technical implementation coordinator.


## Hello World 

Get started by saying hello world to us.

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

When doing HTTP POST requests to the API, a client browser session_id key must be included in the 
JSON payload. Additional data such as client IP address and user agent are recommended to assist 
RootRez in debugging issues.

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

* Use HTTPS. All communication with RootRez is handled over HTTPS.
* Keep your API key out of version control (such as GIT or SVN), instead store in a local config file or similar secure means.
* Cache data that is unlikely to change frequently such as property data (not including rates) 
and publisher settings.
* Use low verbosity levels (0 is lowest, 3 is highest). The less data requested, the faster 
the response.
* Pre-validate customer data such as billing address, email address, and credit card data before making requests to RootRez. While we do validate this information, creating client-side checks for your customers can greatly improve the booking experience.

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

Most exceptions will be accompanied with additional data in the message string. These can be caught in your application and specific, 
user-friendly messages can be created for your end-users.

**RoomUnavailableException**

The requested room is not available for booking.

**BookingValidationException**

Invalid data was received in your booking request

**AddressValidationException**

Any address related errors on a booking request.

**CreditCardException**

Invalid credit card data. Either we couldn’t verify the cardholders account or it failed a 
Luhn algorithm check. You should pre-check credit cards against the Luhn algorithm in your 
implementation.

**RemoteInventoryException**

RootRez was unable to verify the inventory exists in the hotels inventory system or within a 
third-parties inventory system.

**RemoteInformationException**

RootRez was unable to retrieve hotel meta data from the hotels information system and/or 
third party system.

**DuplicateBookingException**

A similar booking has already been processed.
