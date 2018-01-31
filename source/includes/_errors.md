# Errors

The Koïos Smart Insurance API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- The username and password don't match.
403 | Forbidden -- Forbidden access to the page.
404 | Not Found -- The page could not be found.
405 | Method Not Allowed -- You tried to access the API with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
429 | Too Many Requests -- DDOS protection.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
