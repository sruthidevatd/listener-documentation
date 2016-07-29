Listener maintains a basic user record to track user activity and permissions. Listener uses LDAP for authentication; when the user first logs in, a new record is created. The user endpoint gives the list of users. The only change that can be made is to promote a user to an administrator. Only administrators can change or delete a user.

* [User Object](#user-object)
* [Get a List of Users](#get-a-list-of-users)
* [Get a User](#get-a-user)
* [Promote User to Admin](#get-a-list-of-users)
* [Delete a User](#delete-a-user)

## User Object

Property     | Type    | Example | Description
-------------|---------|---------|-------------
display_name | string  | `Doey, Joey` | Name of user.
email        | string  | `jdoey@example.com` | Email address of user.
id           | string  | `jdoey` | User ID of user. Used to bind to LDAP.
site_admin   | boolean | `true` | Permissions of user on Listener.
member_of    | string  | `CN=ALL EMPLOYEES,OU=Groups,DC=ldap,DC=web,DC=com` | LDAP-compliant directories of which user is a member.









## Get a List of Users

Load a list of all users that have logged into Listener.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/users HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -i \
  https://listener-app-services.teradata.com/v1/users
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "display_name": "Doey, Joey",
    "email": "jdoey@example.com",
    "id": "jdoey",
    "site_admin": true,
    "member_of": "CN=ALL EMPLOYEES,OU=Groups,DC=ldap,DC=web,DC=com"
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
200  | Users were returned successfully.
401_STATUS







## Get a User

Get a single user record.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/users/{user_id} HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -i \
  https://listener-app-services.teradata.com/v1/users/jdoey
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
  "display_name": "Doey, Joey",
  "email": "jdoey@example.com",
  "id": "jdoey",
  "site_admin": true,
  "member_of": "CN=ALL EMPLOYEES,OU=Groups,DC=ldap,DC=web,DC=com"
}
```

#### Response Codes

Code | Meaning
---- | -------
200  | User was returned successfully.
401_STATUS








## Promote User to Admin

Admins can promote another user to administrator level, which should be given to only those users who need that level of permission.

#### Definition

```http
PATCH https://listener-app-services.teradata.com/v1/users HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PATCH \
  -d '{
    "site_admin": true
  }' \
  -i \
  https://listener-app-services.teradata.com/v1/users/jdoey
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "display_name": "Doey, Joey",
    "email": "jdoey@example.com",
    "id": "jdoey",
    "site_admin": true,
    "member_of": "CN=ALL EMPLOYEES,OU=Groups,DC=ldap,DC=web,DC=com"
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
200  | Users were returned successfully.
401_STATUS









## Delete a User

Deleting a user will remove them from Listener; however, it does not block them from logging in again if they have valid credentials.

#### Definition

```http
DELETE https://listener-app-services.teradata.com/v1/users/{user_id} HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PATCH \
  -d '{
    "site_admin": true
  }' \
  -i \
  https://listener-app-services.teradata.com/v1/users/jdoey
```

#### Example Response

```http
HTTP/1.1 204 No Content
Content-Type: application/json
```

#### Response Codes

Code | Meaning
---- | -------
204  | User was removed successfully.
401_STATUS
