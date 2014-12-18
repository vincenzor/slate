# Workspaces
## The workspace object
```
# EXAMPLE OBJECT
```
```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "workspace",
  "name": "Personnal",
  "tasks_count": 32,
  "total_planned_tasks": 15,
  "total_open_tasks": 6,
  "total_done_tasks": 11,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Attribute | Description
--------- | -----------
uuid | **string** <br />A universally unique identifier for the workspace
object | **string** *value is "workspace"*
name | **string** <br />The workspace’s name
tasks_count | **integer** <br />The number of tasks linked to this workspace
total_planned_tasks | **integer** <br />The number of tasks in the Snooze Box
total_open_tasks | **integer** <br />The number of tasks in the Task Box
total_done_tasks | **integer** <br />The number of tasks in the Done Box
created_at | **timestamp**
updated_at | **timestamp**

## Create a workspace
```ruby
# DEFINITION
Postpone::Workspace.create()

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

Postpone::Workspace.create(
  :name => "My wedding party"
)
```

```shell
# DEFINITION
POST https://api.postponeapp.com/v1/workspaces

# EXAMPLE
curl -X POST https://api.postponeapp.com/v1/workspaces \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "name=My wedding party"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "workspace",
  "name": "My wedding party",
  "tasks_count": 0,
  "total_planned_tasks": 0,
  "total_open_tasks": 0,
  "total_done_tasks": 0,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Creates a new workspace.

### Arguments
Argument | Description
--------- | -----------
name | **string** — **required**<br />The workspace's name

### Returns
Returns the workspace object.


## Retrieving a workspace
```ruby
# DEFINITION
Postpone::Workspace.retrieve({WORKSPACE_UUID})

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

Postpone::Workspace.retrieve("f90650f8-81e5-11e4-b116-123b93f75cba")
```

```shell
# DEFINITION
GET https://api.postponeapp.com/v1/workspaces/{WORKSPACE_UUID}

# EXAMPLE
curl https://api.postponeapp.com/v1/workspaces/f90650f8-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "workspace",
  "name": "Personnal",
  "tasks_count": 32,
  "total_planned_tasks": 15,
  "total_open_tasks": 6,
  "total_done_tasks": 11,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the workspace to be retrieved.

### Returns
Returns the workspace object.



## Update a workspace
```ruby
# DEFINITION
w = Postpone::Workspace.retrieve({WORKSPACE_UUID})
w.name = {NAME}
...
w.save

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

w = Postpone::Workspace.retrieve("f90650f8-81e5-11e4-b116-123b93f75cba")
w.name = "New workspace name"
w.save
```

```shell
# DEFINITION
PUT https://api.postponeapp.com/v1/workspaces/{WORKSPACE_UUID}

# EXAMPLE
curl -X PUT https://api.postponeapp.com/v1/workspaces/f90650f8-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "name=New workspace name"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "workspace",
  "name": "New workspace name",
  "tasks_count": 0,
  "total_planned_tasks": 0,
  "total_open_tasks": 0,
  "total_done_tasks": 0,
  "created_at": 1417978768,
  "updated_at" : 1517954345
}
```

Updates the specified workspace by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

Argument | Description
--------- | -----------
name | **string** — **optional**<br />The workspace's name

### Returns
Returns the workspace object.


## Delete a workspace
```ruby
# DEFINITION
w = Postpone::Workspace.retrieve({WORKSPACE_UUID})
w.delete

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

w = Postpone::Workspace.retrieve("f90650f8-81e5-11e4-b116-123b93f75cba")
w.delete
```

```shell
# DEFINITION
DELETE https://api.postponeapp.com/v1/workspaces/{WORKSPACE_UUID}

# EXAMPLE
curl -X DELETE https://api.postponeapp.com/v1/workspaces/f90650f8-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "deleted": true,
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba"
}
```

Permanently deletes a workspace. It cannot be undone.

<aside class="warning">
Warning — Deleting a workspace will also delete all tasks listed under that workspace.
</aside>

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the workspace to be deleted.

### Returns
Returns an object with a deleted parameter and the workspace UUID.

## List workspaces
```ruby
# DEFINITION
Postpone::Workspace.all

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

Postpone::Workspace.all
```

```shell
# DEFINITION
GET https://api.postponeapp.com/v1/workspaces

# EXAMPLE
curl https://api.postponeapp.com/v1/workspaces \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
      "object": "workspace",
      "name": "Personnal",
      "tasks_count": 32,
      "total_planned_tasks": 15,
      "total_open_tasks": 6,
      "total_done_tasks": 11,
      "created_at": 1417978768,
      "updated_at": 1417978768
    },
    {
      "uuid": "36998eac-81e7-11e4-b116-123b93f75cba",
      "object": "workspace",
      "name": "Wedding",
      "tasks_count": 5,
      "total_planned_tasks": 15,
      "total_open_tasks": 6,
      "total_done_tasks": 11,
      "created_at": 1417979550,
      "updated_at": 1417979550
    },
    ...
  ]
}
```

Returns a list of workspaces. The workspaces are returned sorted by creation date, with the most recently created workspaces appearing first.

This list is [paginate](#pagination) by 100 records. A `has_more` field that indicate if you should check the next page is returned and can be `true` or `false`.

### Arguments
Parameter | Description
--------- | -----------
limit | **integer** — **optional** *— default is 100* <br />A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
