# Projects
## The project object
```
# EXAMPLE OBJECT
```
```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "project",
  "name": "Personnal",
  "tasks_count": 32,
  "total_planned_tasks": 15,
  "total_open_tasks": 6,
  "total_done_tasks": 11,
  "archived_at": null,
  "archived_by_uuid": null,
  "inbound_email": "123456abcdef98765@taskbox.io",
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Attribute | Description
--------- | -----------
uuid | **string** <br />A universally unique identifier for the project
object | **string** *value is "project"*
name | **string** <br />The project’s name
tasks_count | **integer** <br />The number of tasks linked to this project
total_planned_tasks | **integer** <br />The number of tasks in the Snooze Box
total_open_tasks | **integer** <br />The number of tasks in the Task Box
total_done_tasks | **integer** <br />The number of tasks in the Done Box
archived_at | **timestamp** — *can be null* <br />When the project has been archived
archived_by_uuid  | **string** — *can be null* <br />The user universally unique identifier who archived the project
inbound_email | **string** <br />An inbound email used to create a task from email. The subject will be used as the task and the body as the description of the task.
created_at | **timestamp**
updated_at | **timestamp**

## Create a project
```ruby
# DEFINITION
Postpone::Project.create()

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

Postpone::Project.create(
  :name => "My wedding party"
)
```

```shell
# DEFINITION
POST https://postponeapp.com/api/v1/projects

# EXAMPLE
curl -X POST https://postponeapp.com/api/v1/projects \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "name=My wedding party"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "project",
  "name": "My wedding party",
  "tasks_count": 0,
  "total_planned_tasks": 0,
  "total_open_tasks": 0,
  "total_done_tasks": 0,
  "archived_at": null,
  "archived_by_uuid": null,
  "inbound_email": "123456abcdef98765@taskbox.io",
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Creates a new project.

### Arguments
Argument | Description
--------- | -----------
name | **string** — **required**<br />The project's name

### Returns
Returns the project object.


## Retrieving a project
```ruby
# DEFINITION
Postpone::Project.retrieve({PROJECT_UUID})

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

Postpone::Project.retrieve("f90650f8-81e5-11e4-b116-123b93f75cba")
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "project",
  "name": "Personnal",
  "tasks_count": 32,
  "total_planned_tasks": 15,
  "total_open_tasks": 6,
  "total_done_tasks": 11,
  "archived_at": null,
  "archived_by_uuid": null,
  "inbound_email": "123456abcdef98765@taskbox.io",
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the project to be retrieved.

### Returns
Returns the project object.



## Update a project
```ruby
# DEFINITION
w = Postpone::Project.retrieve({PROJECT_UUID})
w.name = {NAME}
...
w.save

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

w = Postpone::Project.retrieve("f90650f8-81e5-11e4-b116-123b93f75cba")
w.name = "New project name"
w.save
```

```shell
# DEFINITION
PUT https://postponeapp.com/api/v1/projects/{PROJECT_UUID}

# EXAMPLE
curl -X PUT https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "name=New project name"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "object": "project",
  "name": "New project name",
  "tasks_count": 0,
  "total_planned_tasks": 0,
  "total_open_tasks": 0,
  "total_done_tasks": 0,
  "archived_at": null,
  "archived_by_uuid": null,
  "inbound_email": "123456abcdef98765@taskbox.io",
  "created_at": 1417978768,
  "updated_at" : 1517954345
}
```

Updates the specified project by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

Argument | Description
--------- | -----------
name | **string** — **optional**<br />The project's name
archived_by_uuid | **string** — **optional**<br />If you set this parameter the project will be archived and the `archived_at` attribute will be set

### Returns
Returns the project object.


## Delete a project
```ruby
# DEFINITION
w = Postpone::Project.retrieve({PROJECT_UUID})
w.delete

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

w = Postpone::Project.retrieve("f90650f8-81e5-11e4-b116-123b93f75cba")
w.delete
```

```shell
# DEFINITION
DELETE https://postponeapp.com/api/v1/projects/{PROJECT_UUID}

# EXAMPLE
curl -X DELETE https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "deleted": true,
  "uuid": "f90650f8-81e5-11e4-b116-123b93f75cba"
}
```

Permanently deletes a project. It cannot be undone.

<aside class="warning">
Warning — Deleting a project will also delete all tasks listed under that project.
</aside>

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the project to be deleted.

### Returns
Returns an object with a deleted parameter and the project UUID.

## List projects
```ruby
# DEFINITION
Postpone::Project.all

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

Postpone::Project.all
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects

# EXAMPLE
curl https://postponeapp.com/api/v1/projects \
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
      "object": "project",
      "name": "Personnal",
      "tasks_count": 32,
      "total_planned_tasks": 15,
      "total_open_tasks": 6,
      "total_done_tasks": 11,
      "archived_at": null,
      "archived_by_uuid": null,
      "inbound_email": "123456abcdef98765@taskbox.io",
      "created_at": 1417978768,
      "updated_at": 1417978768
    },
    {
      "uuid": "36998eac-81e7-11e4-b116-123b93f75cba",
      "object": "project",
      "name": "Wedding",
      "tasks_count": 5,
      "total_planned_tasks": 15,
      "total_open_tasks": 6,
      "total_done_tasks": 11,
      "archived_at": null,
      "archived_by_uuid": null,
      "inbound_email": "445456abcdef98765@taskbox.io",
      "created_at": 1417979550,
      "updated_at": 1417979550
    },
    ...
  ]
}
```

Returns a list of projects. The projects are returned sorted by creation date, with the most recently created projects appearing first.

This list is [paginate](#pagination) by 100 records. A `has_more` field that indicate if you should check the next page is returned and can be `true` or `false`.

### Arguments
Parameter | Description
--------- | -----------
limit | **integer** — **optional** *— default is 100* <br />A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
