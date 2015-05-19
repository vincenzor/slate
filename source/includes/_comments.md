# Comments
## The comment object
```
# EXAMPLE OBJECT
```
```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "comment",
  "task_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "content": "Here is the content of the comment",
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Attribute | Description
--------- | -----------
uuid | **string** <br />A universally unique identifier for the comment
object | **string** *value is "comment"*
task_uuid | **string** <br />The task universally unique identifier.
user_uuid | **string** <br />The user (creator) universally unique identifier.
content | **string** <br />The comment content
created_at | **timestamp**
updated_at | **timestamp**

## Create a comment
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
task = project.tasks.retrieve({TASK_UUID})
task.comments.create()

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
task = project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
task.comment.create(
  :content => "Here is the content of the comment"
)
```

```shell
# DEFINITION
POST https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}/comments

# EXAMPLE
curl -X POST https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba/comments \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "content=Here is the content of the comment"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "comment",
  "task_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "content": "Here is the content of the comment",
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

Creates a new comment.

### Arguments
Argument | Description
--------- | -----------
content | **string** — **required**<br />The comment's content

### Returns
Returns the comment object.

## Retrieving a comment
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
task = project.tasks.retrieve({TASK_UUID})
task.comments.retrieve({COMMENT_UUID})

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
task = project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
task.comments.retrieve('556gfk96-81e5-11e4-b116-123b93f75cba')
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}/comments/{COMMENT_UUID}

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba/comments/556gfk96-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "comment",
  "task_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "content": "Here is the content of the comment",
  "created_at": 1417978768,
  "updated_at" : 1417978768
}
```

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the comment to be retrieved.

### Returns
Returns the comment object.

## Update a comment
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
task = project.tasks.retrieve({TASK_UUID})
c = task.comments.retrieve({COMMENT_UUID})
c.content = {CONTENT}
...
c.save

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
task = project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
c = task.comments.retrieve('556gfk96-81e5-11e4-b116-123b93f75cba')
c.content = "New content here"
c.save
```

```shell
# DEFINITION
PUT https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}/comments/{COMMENT_UUID}

# EXAMPLE
curl -X PUT https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba/comments/556gfk96-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here" \
  -d "name=New content here"
```

> The above command returns JSON structured like this:

```json
{
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba",
  "object": "comment",
  "task_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
  "user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
  "content": "New content here",
  "created_at": 1417978768,
  "updated_at" : 1517978768
}
```

Updates the specified comment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

Argument | Description
--------- | -----------
content | **string** — **optional**<br />The comment's content

### Returns
Returns the comment object.

## Delete a comment
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
task = project.tasks.retrieve({TASK_UUID})
c = task.comments.retrieve({COMMENT_UUID})
c.delete

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
task = project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
c = task.comments.retrieve('556gfk96-81e5-11e4-b116-123b93f75cba')
c.delete
```

```shell
# DEFINITION
DELETE https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}/comments/{COMMENT_UUID}

# EXAMPLE
curl -X DELETE https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba/comments/556gfk96-81e5-11e4-b116-123b93f75cba \
  -H "Authorization: Bearer pp_api_key_here"
```

> The above command returns JSON structured like this:

```json
{
  "deleted": true,
  "uuid": "556gfk96-81e5-11e4-b116-123b93f75cba"
}
```

Permanently deletes a comment. It cannot be undone.

NOTE: A comment can only be deleted by its creator.

### Arguments
Parameter | Description
--------- | -----------
uuid | **string** — **required** <br />The universally unique identifier of the comment to be deleted.

### Returns
Returns an object with a deleted parameter and the comment UUID.

## List comments
```ruby
# DEFINITION
project = Postpone::Project.retrieve({PROJECT_UUID})
task = project.tasks.retrieve({TASK_UUID})
task.comments

# EXAMPLE
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"

project = Postpone::Project.retrieve('f90650f8-81e5-11e4-b116-123b93f75cba')
task = project.tasks.retrieve('3bd5f844-81e5-11e4-b116-123b93f75cba')
task.comments
```

```shell
# DEFINITION
GET https://postponeapp.com/api/v1/projects/{PROJECT_UUID}/tasks/{TASK_UUID}/comments

# EXAMPLE
curl https://postponeapp.com/api/v1/projects/f90650f8-81e5-11e4-b116-123b93f75cba/tasks/3bd5f844-81e5-11e4-b116-123b93f75cba/comments \
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
      "object": "comment",
      "task_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
      "user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
      "content": "New content here",
      "created_at": 1417978768,
      "updated_at" : 1517978768
    },
    {
      "uuid": "27fa8ee0-d3b9-11e4-8830-0800200c9a66",
      "object": "comment",
      "task_uuid": "f90650f8-81e5-11e4-b116-123b93f75cba",
      "user_uuid": "0b4e001c-81e6-11e4-b116-123b93f75cba",
      "content": "Another comment",
      "created_at": 1445458793,
      "updated_at" : 1445458793
    },
    ...
  ]
}
```

Returns a list of comment. The comment are returned sorted by creation date, with the most recently created comments appearing first.

This list is [paginate](#pagination) by 100 records. A `has_more` field that indicate if you should check the next page is returned and can be `true` or `false`.

### Arguments
Parameter | Description
--------- | -----------
limit | **integer** — **optional** *— default is 100* <br />A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
