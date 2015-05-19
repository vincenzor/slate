# Errors
```
# EXAMPLE OBJECT
```
```json
{
  "error": {
    "type": "invalid_request_error",
    "message": "Unable to save project",
    "parameters": {
      "name": [
        "can't be blank"
      ]
    }
  }
}
```
Postpone uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing, a task cannot be created, etc.), and codes in the 5xx range indicate an error with Postpone's servers.

Not all errors map onto HTTP codes, however. When a request is valid but does not complete successfully (e.g. a task cannot be created), we return a 402 error code.

Attribute | Description
--------- | -----------
type | **string** <br />The error type (see below)
message | **string** <br /> A description of the error
parameters | **string** — *can be null* <br /> The parameters the error relate to if the error is parameters-specific. You can use this to display a message near the correct form field, for example.

### TYPES
Type | Meaning
---------- | -------
invalid_request_error	| Invalid request errors arise when your request has invalid parameters.
api_error	| API errors cover any other type of problem (e.g. a temporary problem with Postpone's servers) and should turn up only very infrequently.

### ERROR CODES
Code | Meaning
---------- | -------
200 | OK -- Everything worked as expected.
400 | Bad Request -- Missing a required parameter or invalid URL.
401 | Unauthorized -- Your API key is wrong
402 | Request Failed -- Parameters were valid but request failed.
404 | Not Found -- The specified resource could not be found
500 | Internal Server Error -- We had a problem with Postpone's servers. Try again later.
503 | Service Unavailable -- Postpone's servers are temporarially offline for maintanance. Please try again later.
