# Tasks
## The task object
```
# EXAMPLE OBJECT
```
```json
{
  "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba",
  "object": "task",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "list_uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "title": "Forget about reminders, just postpone",
  "description": "If a task does not require immediate attention, then it should not be displayed.",
  "status": "inbox",
  "flagged": true,
  "position": 4,
  "email_on_snooze": "contact@postponeapp.com",
  "done_by_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "due_at": 1417976990,
  "done_at": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Attribute | Description
--------- | -----------
uuid | **string** <br />A universally unique identifier for the task
object | **string** *value is "task"*
project_uuid | **string** <br />The project universally unique identifier.
list_uuid | **string** — *can be null* <br />The list universally unique identifier.
title | **string** <br />The task main content
description | **string** — *can be null* <br />The task description
status | **string** <br />Possible values are `planned`, `inbox` or `done`. A task snoozed (hidded from the Task Box for later) is `planned` and moves to `inbox` when it's back in the Task Box. When the user flags the task as done, the status is `done` (and the timestamp of this action is recorded in the `done_at` attribute).
flagged | **boolean** <br />Possible values are `true` or `false`.
position | **integer** <br />This is the position of the task in the [list](#lists).
email_on_snooze | **string** — *can be null* <br />If set, an email is send to the email adress when the status moves from `planned` to `inbox`.
done_by_uuid | **string** — *can be null* <br />The user universally unique identifier who flag the task as `done`.
due_at | **timestamp** — *can be null* <br />When the task will automatically move from status `planned` to `inbox` (go back in the Task Box).
done_at | **timestamp** — *can be null* <br />When the task was flag as done by the user.
created_at | **timestamp**
updated_at | **timestamp**

## Create a task
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.tasks.create()

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"


project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.tasks.create(
  :list_uuid => '556gfk96-81e5-11e4-b116-123b93f75cba',
  :title => "Do not create another to-do app like the existing 1.000",
  :flagged => true
)
```

```shell
# DEFINITION
POST https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks

# EXAMPLE
curl -X POST https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "list_uuid=556gfk96-81e5-11e4-b116-123b93f75cba \
  -d "title=Do not create another to-do app like the existing 1.000" \
  -d flagged=true
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba",
  "object": "task",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "list_uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "title": "Do not create another to-do app like the existing 1.000",
  "description": null,
  "status": "inbox",
  "flagged": true,
  "position": 1,
  "email_on_snooze": null,
  "done_by_uuid": null,
  "due_at": null,
  "done_at": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Creates a new task. If you can choose to put the task in the Task Box (with `status='inbox'`) or in the Snooze Box (with `status='planned'`). If you choose to put the task in the Snooze Box the `due_at` is mandatory.

### Arguments
Argument | Description
--------- | -----------
project_uuid | **string** — **required** <br />The project universally unique identifier.
list_uuid | **string** <br />The list universally unique identifier. If not set, the created task will go in the project's Task Box without being linked to a list.
title | **string** — **required** <br />The task main content
description | **string** <br />The task description
status | **string** — *Default is `inbox`* <br />Possible values are `planned`, `inbox` or `done`. A task snoozed (hidded from the Task Box for later) is `planned` and moves to `inbox` when it's back in the Task Box. When the user flags the task as done, the status is `done` (and the timestamp of this action is recorded in the `done_at` attribute). Note: if you set the status to `planned` you must also provide a `due_at` attribute.
flagged | **boolean** — *Default is `false`* <br />Possible values are `true` or `false`.
position | **integer** <br />This is the position of the task in the [list](#lists). If not set, the created task will go on top of the list (first position).
email_on_snooze | **string** <br />If set, an email is send to the email adress when the status moves from `planned` to `inbox`.
due_at | **timestamp** <br />When the task will automatically move from status `planned` to `inbox` (go back in the Task Box).

### Returns
Returns the task object.

## Retrieving a task
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.tasks.retrieve({TASK_UUID})

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba",
  "object": "task",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "list_uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "title": "Forget about reminders, just postpone",
  "description": "If a task does not require immediate attention, then it should not be displayed.",
  "status": "inbox",
  "flagged": true,
  "position": 4,
  "email_on_snooze": "contact@postponeapp.com",
  "done_by_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "due_at": 1417976990,
  "done_at": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the task to be retrieved.

### Returns
Returns the task object.


## Update a task
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
t = project.tasks.retrieve({TASK_UUID})
t.title = {NEW_CONTENT}
t.description = nil
...
t.save

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
t = project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
t.title = "New task content"
t.description = nil
t.save
```

```shell
# DEFINITION
PUT https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}

# EXAMPLE
curl -X PUT https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "title=New task content" \
  -d description=null
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba",
  "object": "task",
  "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "list_uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "title": "New task content",
  "description": null,
  "status": "inbox",
  "flagged": true,
  "position": 4,
  "email_on_snooze": "contact@postponeapp.com",
  "done_by_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "due_at": 1417976990,
  "done_at": null,
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Updates the specified task by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

Argument | Description
--------- | -----------
list_uuid | **string** <br />The list universally unique identifier. If set to `null`, the created task will go in the project's Task Box without being linked to a list.
title | **string** <br />The task main content
description | **string** <br />The task description
status | **string** <br />Possible values are `planned`, `inbox` or `done`. A task snoozed (hidded from the Task Box for later) is `planned` and moves to `inbox` when it's back in the Task Box. Note: if you set the status to `planned` you must also provide a `due_at` attribute.<br />You can change this attribute to move tasks between the differents Postpone's box (Snooze Box, Task Box and Done Box).
flagged | **boolean** <br />Possible values are `true` or `false`.
position | **integer** <br />This is the position of the task in the [list](#lists). If not set, the created task will go on top of the list (first position).
email_on_snooze | **string** <br />If set, an email is send to the email adress when the status moves from `planned` to `inbox`.
due_at | **timestamp** <br />When the task will automatically move from status `planned` to `inbox` (go back in the Task Box).

### Returns
Returns the task object.

## Delete a task
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
t = project.tasks.retrieve({TASK_UUID})
t.delete

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
t = project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
t.delete
```

```shell
# DEFINITION
DELETE https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}

# EXAMPLE
curl -X DELETE https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "deleted": true,
  "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba"
}
```

Permanently deletes a task. It cannot be undone.

<aside class="warning">
Warning — Deleting a task will also delete all comments listed under that task.
</aside>

### Arguments
Parameter | Description
--------- | -----------
uuid | **integer** — **required** <br />The universally unique identifier of the task to be deleted.

### Returns
Returns an object with a deleted parameter and the task UUID.

## Re-ordering tasks
Updating the position of a task is also possible through the [update endpoint](#update-a-task) by passing an integer between 1 and n in the `position` attribute, where n is the number of task in this list.

## List tasks
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
project.tasks

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"
project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
project.tasks({:list_uuid => "556gfk96-81e5-11e4-b116-123b93f75cba"})
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "list_uuid=556gfk96-81e5-11e4-b116-123b93f75cba"
```

> The above command returns JSON structured like this:

```json
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "uuid": "3bd5f844-81e5-11e4-b116-123b93f75cba",
      "object": "task",
      "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
      "list_uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
      "title": "New task content",
      "description": null,
      "status": "inbox",
      "flagged": true,
      "position": 4,
      "email_on_snooze": "contact@postponeapp.com",
      "done_by_id": "0b4e001c-81e6-11e4-b116-123b93f75cba",
      "due_at": 1417976990,
      "done_at": null,
      "created_at": 1417978768,
      "updated_at" : 1417978768
    },
    {
      "uuid": "89a4bd4e-81e5-11e4-b116-123b93f75cba",
      "object": "task",
      "project_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
      "list_uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
      "title": "Here is another task",
      "description": null,
      "status": "inbox",
      "flagged": true,
      "position": 4,
      "email_on_snooze": "contact@postponeapp.com",
      "done_by_id": "0b4e001c-81e6-11e4-b116-123b93f75cba",
      "due_at": 1417976990,
      "done_at": null,
      "created_at": 1417978768,
      "updated_at" : 1417978768
    },
    ...
  ]
}
```

Returns a list of tasks. The tasks are returned sorted by `position`, from 1 to n.

This list is [paginate](#pagination) by 100 records. A `has_more` field that indicate if you should check the next page is returned and can be `true` or `false`.

### Arguments
Parameter | Description
--------- | -----------
list_uuid | **string** — **optional** <br />Get the tasks from a particular list. If you only want to retrieve tasks not linked to a particular list pass `list_uuid=null`
term | **string** — **optional** <br />Get the tasks responding to search `term`.
user_uuid | **string** — **optional** <br />Get the tasks where a user is mentionned (@user).
status | **string** — **optional** <br />Get the tasks in a particular status. Possible values are `planned`, `inbox` or `done`.
limit | **integer** — **optional** *— default is 100* <br />A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
