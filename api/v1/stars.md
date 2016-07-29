When you create a source it is automatically starred, making it a favorite. You can view a list of only starred sources, and you can unstar a source.

* [Star Object](#star-object)
* [Star a Source](#star-a-source)
* [Unstar a Source](#unstar-a-source)
* [Get Starred State](#get-starred-state)

## Star Object

A source contains the following properties.

Property    | Type    | Example | Description
------------|---------|---------|------------
starred     | boolean | `true`  | If the item is starred or not.

All properties are __Read-Only__.

## Star a Source

Star a source for the current user. The user is assumed from the token provided.

#### Definition

```http
PUT https://listener-app-services.teradata.com/v1/sources/{source_id}/star HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PUT \
  -i \
  https://listener-app-services.teradata.com/v1/sources/758fbda4-accc-4f90-8f09-cc0a164c8c28/star
```

#### Example Response

```http
HTTP/1.1 201 Created
Content-Type: application/json
```

#### Response Codes

Code | Meaning
---- | -------
201  | Source was starred successfully.
401_STATUS

## Unstar a Source

Unstar a source for the current user. The user is assumed from the token provided.

#### Definition

```http
DELETE https://listener-app-services.teradata.com/v1/sources/{source_id}/star HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X DELETE \
  -i \
  https://listener-app-services.teradata.com/v1/sources/758fbda4-accc-4f90-8f09-cc0a164c8c28/star
```

#### Example Response

```http
HTTP/1.1 204 No Content
```

#### Response Codes

Code | Meaning
---- | -------
204  | Star was deleted successfully.
401_STATUS


## Get Starred State

Get the starred state for a given source based on the current user's token.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/sources/{source_id}/star HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -i \
  https://listener-app-services.teradata.com/v1/sources/758fbda4-accc-4f90-8f09-cc0a164c8c28/star
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
  "starred": true
}
```

#### Response Codes

Code | Meaning
---- | -------
200  | Sources were returned successfully.
401_STATUS
