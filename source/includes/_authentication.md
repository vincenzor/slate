# Authentication

```ruby
# To authorize, use this code:
>> require 'postpone'
Postpone.api_key = "pp_api_key_here"
```

```shell
# To authorize, use this code:
curl https://api.postponeapp.com/v1 \
  -u pp_api_key_here:
```

> Make sure to replace `pp_api_key_here` with your API key.

You authenticate to the postpone API by providing your API key in the request. You can find your API key [in your account](https://postponeapp.com/api). Be sure to keep your key secret!

Authentication to the API occurs via HTTP Basic Auth. Provide your API key as the basic auth username. You do not need to provide a password.

All API requests must be made over [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure). Calls made over plain HTTP will fail. You must authenticate for all requests.
