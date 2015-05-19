# Authentication

```ruby
# To authorize, use this code:
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"
```

```shell
# To authorize, use this code:
curl https://postponeapp.com/api/v1 \
  -H "Authorization: Bearer pp_api_key_here"
```

> Make sure to replace `pp_api_key_here` with your API key.

You authenticate to the Postpone API by providing your API key in the request. You can find your API key [in your account](https://postponeapp.com/tools). Be sure to keep your key secret!

Authentication to the API occurs via the HTTP `HTTP_AUTHORIZATION` header. Provide your API key as a Bearer token.

All API requests must be made over [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure). Calls made over plain HTTP will fail. You must authenticate for all requests.
