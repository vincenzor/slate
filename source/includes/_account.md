# Account
## The account object

```
# EXAMPLE OBJECT
```
```json
{
  "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba",
  "object": "account",
  "email": "contact@postponeapp.com",
  "firstname": "Vincenzo",
  "lastname": "Ruggiero",
  "time_zone": "Brussels",
  "inbound_email": "123456abcdef98765@taskbox.io"
}
```

Attribute | Description
--------- | -----------
uuid | **string** <br />A universally unique identifier for the account
object | **string** *value is "account"*
email | **string** <br />The user’s email address
firstname | **string** <br />**optional** <br />The user’s firstname
lastname | **string** <br />**optional** <br />The user’s lastname
time_zone | **string** <br />The user time_zone
inbound_email | **string** <br />An inbound email used to create a task from email

## Retrieve account details
```ruby
# DEFINITION
Postpone::Account.retrieve()

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

Postpone::Account.retrieve()
```

```shell
# DEFINITION
GET https://api.postponeapp.com/v1/account

# EXAMPLE
curl https://api.postponeapp.com/v1/account \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba",
  "object": "account",
  "email": "contact@postponeapp.com",
  "firstname": "Vincenzo",
  "lastname": "Ruggiero",
  "time_zone": "Brussels",
  "inbound_email": "123456abcdef98765@taskbox.io"
}
```

### Arguments
*No arguments*
