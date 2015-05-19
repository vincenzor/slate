# Invitations
## The invitation object
```
# EXAMPLE OBJECT
```
```json
{
  "uuid": "78c1d7d4-8206-11e4-b116-123b93f75cba",
  "object": "invitation",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "status": "accepted",
  "access_level": "admin",
  "email": "contact@postponeapp.com",
  "responded_by_user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "message": "Hi, \nI would like to share the project My Wedding with you on Postpone.",
  "responded_at": 1417978985,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

An invitation is used to invite someone to collaborate with you on a particular [project](#projects). When sending an invitation, an email will be send to the email adress you provide inviting the person to join and get acces to the project.

Attribute | Description
--------- | -----------
uuid | **string** <br />A universally unique identifier for the invitation
object | **string** *value is "invitation"*
project_uuid | **string** <br />The project universally unique identifier.
status | **string** <br />Possible values are `pending`, `accepted` or `rejected`. When the user responds to invitation, the status goes from `pending` to `accepted` or `rejected` (and the timestamp of this action is recorded in the `responded_at` attribute).
access_level | **string** <br />Possible values are `admin` or `write`. The `admin` access level means that the user will be able to create other invitations to the specific project.
email | **string** <br />The email where the invitation was originally sent.
responded_by_user_uuid | **string** — *can be null* <br />The user universally unique identifier who responded to the invitation.
message | **string** — *can be null* <br />A personal message sent with the invitation.
responded_at | **timestamp** — *can be null* <br />When the invitation was accepted or rejected by the user.
created_at | **timestamp**
updated_at | **timestamp**

## Create an invitation
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.invitations.create()

Postpone::Invitation.create(
  :email => {EMAIL}
)

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.invitations.create(
  :email => "contact@postponeapp.com"
)
```

```shell
# DEFINITION
POST https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/invitations

# EXAMPLE
curl -X POST https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/invitations \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "email=contact@postponeapp.com"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "78c1d7d4-8206-11e4-b116-123b93f75cba",
  "object": "invitation",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "status": "pending",
  "access_level": "write",
  "email": "contact@postponeapp.com",
  "responded_by_user_uuid": null,
  "message": null,
  "responded_at": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Creates a new invitation.

### Arguments
Argument | Description
--------- | -----------
project_uuid | **string** — **required**<br />The project universally unique identifier.
email | **string** — **required**<br />The email where to send the invitation.
access_level | **string** — *Default is `write`*<br />Possible values are `admin` or `write`. The `admin` access level means that the user will be able to create other invitations to the specific project.
message | **string** <br />A personal message to add in the invitation.

### Returns
Returns the invitation object.


## Retrieving an invitation
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.invitations.retrieve({INVITATION_UUID})

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.invitations.retrieve("78c1d7d4-8206-11e4-b116-123b93f75cba")
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/invitations/{INVITATION_UUID}

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/invitations/78c1d7d4-8206-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "78c1d7d4-8206-11e4-b116-123b93f75cba",
  "object": "invitation",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "status": "pending",
  "access_level": "write",
  "email": "contact@postponeapp.com",
  "responded_by_user_uuid": null,
  "message": null,
  "responded_at": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the invitation to be retrieved.

### Returns
Returns the invitation object.



## Update an invitation
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
i = project.invitations.retrieve({INVITATION_UUID})
i.status = {NEW_STATUS}
...
i.save

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
i = project.invitations.retrieve("78c1d7d4-8206-11e4-b116-123b93f75cba")
i.status = "accepted"
i.responded_by_user_uuid = "0b4e001c-81e6-11e4-b116-123b93f75cba"
i.save
```

```shell
# DEFINITION
PUT https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/invitations/{INVITATION_UUID}

# EXAMPLE
curl -X PUT https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/invitations/78c1d7d4-8206-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "status=accepted"
  -d "responded_by_user_uuid=0b4e001c-81e6-11e4-b116-123b93f75cba"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "78c1d7d4-8206-11e4-b116-123b93f75cba",
  "object": "invitation",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "status": "accepted",
  "access_level": "write",
  "email": "contact@postponeapp.com",
  "responded_by_user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "message": null,
  "responded_at": 1417978985,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Updates the specified invitation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

Argument | Description
--------- | -----------
status | **string** — **optional**<br />Possible values are `accepted` or `rejected`.
access_level | **string** — **optional**<br />Possible values are `admin` or `write`. The `admin` access level means that the user will be able to create other invitations to the specific project.

### Returns
Returns the invitation object.


## Delete an invitation
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
i = project.invitations.retrieve({INVITATION_UUID})
i.delete

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
i = project.invitations.retrieve("78c1d7d4-8206-11e4-b116-123b93f75cba")
i.delete
```

```shell
# DEFINITION
DELETE https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/invitations/{INVITATION_UUID}

# EXAMPLE
curl -X DELETE https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/invitations/78c1d7d4-8206-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "deleted": true,
  "uuid": "78c1d7d4-8206-11e4-b116-123b93f75cba"
}
```

Permanently deletes an invitation. It cannot be undone. The user who received the invitation by email will not be able to answer anymore. Note: You can only delete invitation with status `pending`.

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the invitation to be deleted.

### Returns
Returns an object with a deleted parameter and the invitation UUID.

## List invitations
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.invitations

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.lists
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/invitations

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/invitations \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "object": "list",
  "has_more": false,
  "data": [
  {
    "uuid": "78c1d7d4-8206-11e4-b116-123b93f75cba",
    "object": "invitation",
    "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
    "status": "accepted",
    "access_level": "write",
    "email": "contact@postponeapp.com",
    "responded_by_user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
    "message": null,
    "responded_at": 1417978985,
    "created_at": 1417978768,
    "updated_at" : 1417978768
  },
  {
    "uuid": "055726ac-8209-11e4-b116-123b93f75cba",
    "object": "invitation",
    "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
    "status": "pending",
    "access_level": "admin",
    "email": "support@postponeapp.com",
    "responded_by_user_uuid": null,
    "message": null,
    "responded_at": null,
    "created_at": 1417978768,
    "updated_at" : 1417978768
  },
  ...
  ]
}
```

Returns a list of invitations. The invitations are returned sorted by creation date, with the most recently created invitations appearing first.

This list is [paginate](#pagination) by 100 records. A `has_more` field that indicate if you should check the next page is returned and can be `true` or `false`.

### Arguments
Parameter | Description
--------- | -----------
limit | **integer** — **optional** *— default is 100* <br />A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
status | **string** — **optional** <br />Get the invitations in a particular status. Possible values are `pending`, `accepted` or `rejected`.
access_level | **string** — **optional** <br />Get the invitations of a particular access level. Possible values are `admin` or `write`.
