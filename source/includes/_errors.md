# Errors

<aside class="notice">
Here is how to interpret errors you might encounter. <code>error</code>. Errors below are no reason for panic.
</aside>

The RAYPACK API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The model requested is for administrators only.
404 | Not Found -- The specified model could not be found.
405 | Method Not Allowed -- You tried to access a model with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json or jpeg.
410 | Gone -- The model requested has been removed from our servers.
429 | Too Many Requests -- You're running too many models at once! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
