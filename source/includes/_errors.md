# Errors

The Lumiform Public API uses the following error codes:


Error Code | Meaning
---------- | -------
401 | Unauthorized -- Your API key is wrong.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access a resource with an invalid method.
406 | Not Acceptable -- You requested a format that isn't JSON.
422 | Unprocessable Entity -- Your filters are incorrectly specified. Check the examples!
429 | Too Many Requests -- You're requesting too many resources! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
