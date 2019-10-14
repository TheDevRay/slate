# Authentication / Authorization

> To authorize, use this code:

```javascript
  // You can just pass the correct header with each request
  var options = {
    url: 'http://localhost/api/v1/<authorized_endpoint>',
    headers: {
      'Authorization': 'Bearer <GENERATED_ACCESS_TOKEN>'
    }
  };

  request(options, function (error, response) {
    if (error) throw new Error(error);

    console.log(body);
  });
```

> Make sure to replace `<GENERATED_ACCESS_TOKEN>` with your API key.

For most routes you MUST be authenticated to the the API.

Using the headers in your prefered method, add the following:

`Authorization: Bearer <GENERATED_ACCESS_TOKEN>`

<aside class="notice">
You must replace <code>< GENERATED_ACCESS_TOKEN ></code> with the responded token from the server.
</aside>
<aside class="warning">
If an endpoint requires authentication and it has no valid user, a <code>401 Unauthorized</code> will be thrown.
</aside>
<aside class="warning">
If an endpoint is not available for a given user, a <code>403 Forbidden</code> will be thrown.
</aside>

## Authenticate a user

```javascript
  var request = require("request");

  var options = {
    method: 'POST',
    url: 'http://localhost/api/v1/auth/login',
    body: '{
      email: "user@example.com",
      password: "P@ssw0rd."
    }'
  };

  request(options, function (error, response, body) {
    if (error) throw new Error(error);

    console.log(body);
  });
```

> The above command returns JSON structured like this:

```json
{
    "message": null,
    "data": {
        "auth": {
            "access_token": "<GENERATED_ACCESS_TOKEN>",
            "token_type": "bearer",
            "expires_in": 3600
        }
    },
    "errors": []
}
```

This endpoint sign a user in.

### HTTP Request

`POST http://localhost/api/v1/auth/login`

### Form Parameters

All these parameters are required.

Parameter | Description
 -------- | -----------
email | The user's email address.
password | The prefered password.

## Refresh token

```javascript
  var options = {
    method: 'POST',
    url: 'http://localhost/api/v1/auth/refresh',
    headers: {
      'Authorization': 'Bearer <GENERATED_AUTH_TOKEN>
    }',
    body: '{"email": "user@example.com", "password": "SuperSecret"}
  };

  request(options, function (error, response) {
    if (error) throw new Error(error);

    console.log(body);
  });
```

> The above command returns JSON structured like this:

```json
{
    "message": null,
    "data": {
        "auth": {
            "access_token": "<GENERATED_ACCESS_TOKEN>",
            "token_type": "bearer",
            "expires_in": 3600
        }
    },
    "errors": []
}
```

This should get you a whole new bearer token.

### HTTP Request

`POST http://localhost/api/v1/auth/refresh`

## Logout

```javascript
  var request = require("request");

  var options = {
    method: 'POST',
    url: 'http://localhost/api/v1/auth/logout',
    headers: {
      'Authorization': 'Bearer <GENERATED_AUTH_TOKEN>
    }'
  };

  request(options, function (error, response) {
    if (error) throw new Error(error);

    console.log(body);
  });
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successfully logged out",
  "data": [],
  "errors": []
}
```

Logging out the logged in user. Although this shouldn't happen very often, we still need implement it.

### HTTP Request

`POST http://localhost/api/v1/auth/logout`

## Get the authenticated user

```javascript
  var request = require("request");

  var options = {
    method: 'GET',
    url: 'http://localhost/api/v1/auth/me',
    headers: {
      'cache-control': 'no-cache',
      'Content-Type': 'application/json',
      'X-Requested-With': 'XMLHttpRequest',
      'Authorization': 'Bearer <GENERATED_AUTH_TOKEN>
    }'
  };

  request(options, function (error, response) {
    if (error) throw new Error(error);

    console.log(body);
  });
```

> The above command returns JSON structured like this:

```json
{
  "message": null,
  "data": {
    "id": 1001,
    "me": true,
    "name": "User",
    "email": "user@example.com",
    "verified": false,
    "role": "User",
    "profile": {
      "age": 38,
      "date_of_birth": "1980-12-31"
    },
    "links": {
      "profile": "http://localhost/api/v1/auth/profile/1001"
    },
    "auth": {
      "access_token": "<GENERATED_AUTH_TOKEN>",
      "token_type": "bearer",
      "expires_in": 3600
    }
  },
  "errors": []
}
```

Get the current signed in user.

### HTTP Request

`GET http://localhost/api/v1/auth/me`

