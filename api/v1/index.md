The Teradata Listener REST API allows command, control and monitoring of a Teradata Listener installation.

The REST API manages entities in Listener, such as sources, users, and targets, and provides additional information about the behavior and health of Listener.

## Base URL

The REST API has its own hostname, which varies across Listener installations. It is customized during the installation of Listener and set by the administrator. Typically, it follows this format:

    https://listener-app-services.YOURCOMPANY.DOMAIN/v1/

Ask your administrator for the proper domain for your installation.

## Versioning

The API is versioned and it is recommended that you use `/v1/` in the path to denote the specific version to use. If you do not use the version path, then it will default to the most recent version of the API.

When breaking changes are made to the API, they are released as a new version. Using a specific version should prevent errors in your applications from changes to the API.

## Authentication
All API requests require a valid `Authorization` header, except the Login endpoint. The header requires a valid token. To obtain a valid token, authenticate by sending a request to the [User Login endpoint](authentication.md).

```http
Authorization: Bearer VALID_TOKEN
```

Certain endpoints are valid only for Administrator users, and require a token obtained during login using Administrator credentials. If a user is promoted to Administrator, they must obtain a new token to access Administrator features.

The token is valid for 5 days from the time it is issued. Once the token expires, delete the cache or stored copy and obtain a new token.

Some endpoints are valid only for the Super User, and require a token obtained during login using Super User credentials.

## Media Types
The API accepts and returns the `application/json` media type for all requests. We recommend you declare a `Content-Type: application/json` header in requests. Requests with a message-body use plain JSON to set or update resource states.

## CORS Support
The API supports CORS requests, which allows browsers to call the API directly from other domains.

## IDs

All records are given an id in the form of a [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier). Anywhere you see a string like `758fbda4-accc-4f90-8f09-cc0a164c8c28`, this is an id for an entity in the form of a UUID.

## Timestamps

All timestamps are expected to be compliant with [RFC3339](https://www.ietf.org/rfc/rfc3339.txt) in the format of `YYYY-MM-DDTHH:MM:SSZ`. All timestamps are in GMT and not localized; however, if you view a record in the Listener UI, the browser may modify the date displayed for your local time zone.

## Error States
Listener uses the common [HTTP Response Status Codes](https://github.com/for-GET/know-your-http-well/blob/master/status-codes.md). Additional verbose error messages are supplied in the body response where applicable.
