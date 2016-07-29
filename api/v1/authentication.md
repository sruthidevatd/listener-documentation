To use any REST endpoint, you must first log into Listener and obtain a token. Listener uses configured LDAP servers to authenticate, so a user must be in a correctly configured LDAP group to obtain a token.

### Definition

```http
POST https://listener-app-services.teradata.com/v1/users/login HTTP/1.1
Content-Type: application/json

{
  "username": "YOUR_USERNAME",
  "password": "YOUR_PASSWORD"
}
```

### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{"username": "USERNAME", "password": "PASSWORD"}' \
  -i \
  https://listener-app-services.teradata.com/v1/users/login
```

### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
  "display_name": "name",
  "email": "email",
  "id": "username",
  "member_of": "member of list",
  "site_admin":true,
  "token":"unique token"
}  
```

### Response Codes

Code | Meaning
---- | -------
200  | User successfully logged in and obtained a token.
401  | User's credentials could not be validated.
500  | LDAP is not configured or reachable.
