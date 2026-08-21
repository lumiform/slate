# Errors

The Lumiform Public API uses the following error codes:


Error Code | Meaning
---------- | -------
401 | Unauthorized -- Your API key is wrong.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access a resource with an invalid method.
406 | Not Acceptable -- You requested a format that isn't JSON.
422 | Unprocessable Entity -- Your filters or your request body are incorrectly specified. See Validation Errors below.
429 | Too Many Requests -- You're requesting too many resources! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

## Validation Errors

> A `422` response is structured like this:

```json
{
  "code": "api.validation.errors",
  "message": "The given data was invalid.",
  "errors": {
    "users": ["validation.entityFolderSeatManagement.noFreeSeats"]
  }
}
```

A `422` response carries an `errors` object keyed by the field that caused the failure. Each value is a
list of stable error codes.

Match on the codes, not on `message`. The `message` text is localised and may change; the codes will not.

### Seat limit codes

Your organization's parent can enable **seat management** for entity folders. When it is enabled, a
top-level entity folder can carry a seat limit, set from the Lumiform web app. While a limit is in force,
writes that change who can reach that folder are checked against the capacity of the resulting state.

Code | Field | Meaning
---- | ----- | -------
`validation.entityFolderSeatManagement.noFreeSeats` | `users`, or `role` on user writes | The resulting assignments cannot all be charged against the folder's remaining seats. Assign fewer users, or free a seat by removing someone else, or raise the limit in the web app.
`validation.entityFolderSeatManagement.limitedFolderCannotBeNested` | `children` | A folder that carries a seat limit cannot become a child of another folder. Remove the limit in the web app first, then nest it.

These codes can be returned by write requests on entity folders, entity items, entity types and users.
They are business errors: correct the request before retrying, and do not retry it unchanged.

<aside class="notice">
Seat limits are managed in the Lumiform web app. They are not readable or writable through the Public API,
and no request field of yours is involved -- a request that does not change folder reachability is never
affected. Organizations without seat management enabled never receive these codes.
</aside>
