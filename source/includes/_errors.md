# Errors

The Spouser API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The user is not authenticated to access this route.
404 | Not Found -- The specified user could not be found.
405 | Method not allowed -- You requested a method that doesn't like to do this.
422 | Unprocessable Entity -- Form validation error.
429 | Too Many Requests -- Too many requestes! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
