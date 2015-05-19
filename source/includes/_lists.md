# Lists
## The list object
```
# EXAMPLE OBJECT
```
```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "list",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "name": "Personnal",
  "tasks_count": 13,
  "total_planned_tasks": 5,
  "total_open_tasks": 8,
  "total_done_tasks": 4,
  "archived_at": null,
  "archived_by_uuid": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Attribute | Description
--------- | -----------
uuid | **string** <br />A universally unique identifier for the list
object | **string** *value is "list"*
project_uuid | **string** <br />The project universally unique identifier.
name | **string** <br />The list's name
tasks_count | **integer** <br />The number of tasks linked to this list
total_planned_tasks | **integer** <br />The number of tasks in the Snooze Box
total_open_tasks | **integer** <br />The number of tasks in the Task Box
total_done_tasks | **integer** <br />The number of tasks in the Done Box
archived_at | **timestamp** — *can be null* <br />When the list has been archived
archived_by_uuid  | **string** — *can be null* <br />The user universally unique identifier who archived the list
created_at | **timestamp**
updated_at | **timestamp**

## Create a list
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.lists.create()

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.lists.create(
  :name => "My wedding party"
)
```

```shell
# DEFINITION
POST https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/lists

# EXAMPLE
curl -X POST https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/lists \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "name=My wedding party"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "list",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "name": "My wedding party",
  "tasks_count": 0,
  "total_planned_tasks": 0,
  "total_open_tasks": 0,
  "total_done_tasks": 0,
  "archived_at": null,
  "archived_by_uuid": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Creates a new list.

### Arguments
Argument | Description
--------- | -----------
name | **string** — **required**<br />The list's name

### Returns
Returns the list object.


## Retrieving a list
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.lists.retrieve({LIST_UUID})

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.lists.retrieve('556gfk96-81e5-11e4-b116-123b93f75cba')
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/lists/{LIST_UUID}

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/lists/556gfk96-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "list",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "name": "Personnal",
  "tasks_count": 13,
  "total_planned_tasks": 5,
  "total_open_tasks": 8,
  "total_done_tasks": 4,
  "archived_at": null,
  "archived_by_uuid": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the list to be retrieved.

### Returns
Returns the list object.



## Update a list
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
l = project.lists.retrieve({LIST_UUID})
l.name = {NAME}
...
w.save

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
l = project.lists.retrieve('556gfk96-81e5-11e4-b116-123b93f75cba')
l.name = "New list name"
l.save
```

```shell
# DEFINITION
PUT https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/lists/{LIST_UUID}

# EXAMPLE
curl -X PUT https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/lists/556gfk96-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "name=New list name"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "list",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "name": "New list name",
  "tasks_count": 0,
  "total_planned_tasks": 0,
  "total_open_tasks": 0,
  "total_done_tasks": 0,
  "archived_at": null,
  "archived_by_uuid": null,
  "created_at": 1417978768,
  "updated_at" : 1517954345
}
```

Updates the specified list by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

Argument | Description
--------- | -----------
name | **string** — **optional**<br />The list's name
project_uuid | **string** — **optional**<br />Move the list into a different project.
archived_by_uuid | **string** — **optional**<br />If you set this parameter the list will be archived and the `archived_at` attribute will be set

### Returns
Returns the list object.


## Delete a list
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
l = project.lists.retrieve({LIST_UUID})
l.delete

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
l = project.lists.retrieve('556gfk96-81e5-11e4-b116-123b93f75cba')
l.delete
```

```shell
# DEFINITION
DELETE https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/lists/{LIST_UUID}

# EXAMPLE
curl -X DELETE https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/lists/556gfk96-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "deleted": true,
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba"
}
```

Permanently deletes a list. It cannot be undone.

<aside class="warning">
Warning — Deleting a list will also delete all tasks listed under that list.
</aside>

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the list to be deleted.

### Returns
Returns an object with a deleted parameter and the list UUID.

## List lists
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.lists

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.lists
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/lists

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/lists \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
      "object": "list",
      "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
      "name": "Personnal",
      "tasks_count": 13,
      "total_planned_tasks": 5,
      "total_open_tasks": 8,
      "total_done_tasks": 4,
      "archived_at": null,
      "archived_by_uuid": null,
      "created_at": 1417978768,
      "updated_at": 1417978768
    },
    {
      "uuid": "7600v6ac-45a8-11e4-b116-123b93f75cba",
      "object": "list",
      "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
      "name": "Wedding",
      "tasks_count": 3,
      "total_planned_tasks": 7,
      "total_open_tasks": 4,
      "total_done_tasks": 7,
      "archived_at": null,
      "archived_by_uuid": null,
      "created_at": 1417979550,
      "updated_at": 1417979550
    },
    ...
  ]
}
```

Returns a list of lists. The lists are returned sorted by creation date, with the most recently created lists appearing first.

This list is [paginate](#pagination) by 100 records. A `has_more` field that indicate if you should check the next page is returned and can be `true` or `false`.

### Arguments
Parameter | Description
--------- | -----------
limit | **integer** — **optional** *— default is 100* <br />A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
