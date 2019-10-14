# Users

## Register a user

```javascript
  var request = require("request");

  var options = {
    method: 'POST',
    url: 'http://localhost/api/v1/register',
    headers: {
      'cache-control': 'no-cache',
      // 'Content-Type': 'application/json',
      'Content-Type': 'application/x-www-form-urlencoded',
      'X-Requested-With': 'XMLHttpRequest'
    },
    body: '{
      name: "user",
      email: "user@example.com",
      password: "P@ssw0rd.",
      password_confirmation: "P@ssword.",
      gender_id: "1",
      feels_gender_id: "1",
      search_gender_id: "1",
      date_of_birth: "1980-12-31",
      privacy_statement: "1",
      terms_and_conditions: "1"
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

**TODO** Register post json checken.

This endpoint registers a user.
If there are no errors thrown, the user will automatically be singed in.

### HTTP Request

`POST http://localhost/api/v1/register`

### Form Parameters

All these parameters are required.

Parameter | Description | Available options
 -------- | ----------- | -----------------
name | The username.
email | The user's email address.
password | The prefered password.
password_confirmation | The user's needs to validate the given password.
gender_id | The prefered gender. | 1) male, 2) female, 3) other/both
feels_gender_id | Which gender the user feels like. | 1) male, 2) female, 3) other/both
search_gender_id | The initial gender to search on. | 1) male, 2) female, 3) other/both
date_of_birth | The date of birth. | Formatted like `yyyy-mm-dd`
terms_and_conditions | User must accepted these.
privacy_statement | User must accept this.
