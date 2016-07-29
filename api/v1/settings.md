The settings endpoint allows you to manage configuration of Listener LDAP settings.

* [LDAP Settings Object](#ldap-settings-object)
* [Get LDAP Settings](#get-ldap-settings)
* [Update LDAP Settings](#update-ldap-settings)
* [Test LDAP Setting](#test-ldap-setting)

## LDAP Settings Object

The LDAP server setting object includes the following properties:

Property        | Type    | Example | Description
-------------   |---------|---------|-------------
base_dn         | string  | `ou=Users,DC=ldap,DC=web,DC=com` | LDAP compliant Base DN for performing searches.
email_field     | string  | `mail` | Map LDAP property for user's email.
encryption      | string  | `tls` | Encryption method for connecting to LDAP server. Currently `tls` or `none`.
member_of_field | string  | `memberOf` | Map LDAP property for user's member field.
name            | string  | `my LDAP server` | Custom name of LDAP server.
name_field      | string  | `display_name` | Map LDAP property for user's name.
port            | int     | `389` | LDAP server port.
search_pass     | string  | `secret123` | Password of search user.  Returns encrypted value.
search_user     | string  | `cn=ab123456,ou=Users,DC=ldap,DC=web,DC=com` | Full DN of user who will be used to search.
server          | string  | `ldap.web.com` | LDAP server address.
test_cn         | string  | `ip123456` | Test user name to validate connection.  Not returned by API or stored.
validate_ssl    | bool    | `false` | Option to validate LDAP encryption certificate.






## Get LDAP settings

Get the LDAP settings.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/admin/settings/ldap HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -i \
  https://listener-app-services.teradata.com/v1/admin/settings/ldap
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "base_dn": "ou=Users,DC=ldap,DC=web,DC=com",
    "email_field": "mail",
    "encryption": "tls",
    "member_of_field": "memberOf",
    "name": "my LDAP server",
    "name_field": "name",
    "port": 389,
    "search_pass": "password",
    "search_user": "cn=ab123456,ou=Users,DC=ldap,DC=web,DC=com",
    "server": "ldap.web.com",
    "validate_ssl": false
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
200  | Settings were returned successfully.
401_STATUS







## Update LDAP Settings

Update the LDAP settings array. Ensure you send all records back, or you might remove existing records. To delete a LDAP record, remove it from the array and update it.

#### Definition

```http
PATCH https://listener-app-services.teradata.com/v1/admin/settings/ldap HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PATCH \
  -d '[
    {
      "base_dn": "ou=Users,DC=ldap,DC=web,DC=com",
      "email_field": "mail",
      "encryption": "tls",
      "member_of_field": "memberOf",
      "name": "my LDAP updated server",
      "name_field": "name",
      "port": 389,
      "search_pass": "password",
      "search_user": "cn=ab123456,ou=Users,DC=ldap,DC=web,DC=com",
      "server": "ldap.web.com",
      "validate_ssl": false
    }
  ]' \
  -i \
  https://listener-app-services.teradata.com/v1/admin/settings/ldap
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "base_dn": "ou=Users,DC=ldap,DC=web,DC=com",
    "email_field": "mail",
    "encryption": "tls",
    "member_of_field": "memberOf",
    "name": "my LDAP updated server",
    "name_field": "name",
    "port": 389,
    "search_pass": "password",
    "search_user": "cn=ab123456,ou=Users,DC=ldap,DC=web,DC=com",
    "server": "ldap.web.com",
    "validate_ssl": false
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
200  | Settings were updated successfully.
401_STATUS







## Test LDAP Setting

This allows you to test a single LDAP object before storing it, to ensure it can connect successfully. Send only a single object, not an array of objects. Pass a `test_cn` property with a valid CN to use to query.

#### Definition

```http
POST https://listener-app-services.teradata.com/v1/admin/settings/ldap HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X POST \
  -d '{
      "base_dn": "ou=Users,DC=ldap,DC=web,DC=com",
      "email_field": "mail",
      "encryption": "tls",
      "member_of_field": "memberOf",
      "name": "my LDAP updated server",
      "name_field": "name",
      "port": 389,
      "search_pass": "password",
      "search_user": "cn=ab123456,ou=Users,DC=ldap,DC=web,DC=com",
      "server": "ldap.web.com",
      "test_cn": "cn=ab123456,ou=Users,DC=ldap,DC=web,DC=com",
      "validate_ssl": false
    }' \
  -i \
  https://listener-app-services.teradata.com/v1/admin/settings/ldap
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
  "base_dn": "ou=Users,DC=ldap,DC=web,DC=com",
  "email_field": "mail",
  "encryption": "tls",
  "member_of_field": "memberOf",
  "name": "my LDAP updated server",
  "name_field": "name",
  "port": 389,
  "search_pass": "password",
  "search_user": "cn=ab123456,ou=Users,DC=ldap,DC=web,DC=com",
  "server": "ldap.web.com",
  "validate_ssl": false
}
```

#### Response Codes

Code | Meaning
---- | -------
200  | Successfully connected to LDAP.
400  | Could not connect to LDAP settings.
401_STATUS
