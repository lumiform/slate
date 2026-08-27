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
  "message": "{\"type\":\"validation.code\",\"parameters\":[]}",
  "errors": [
    {
      "type": "validation.code",
      "parameters": [],
      "field": "fieldName"
    }
  ],
  "code": 422
}
```

A `422` response carries an `errors` array of error objects. Each object has `type`, `parameters` and
`field`. `errors` is always a numeric array — never an object keyed by field name.

Match on `errors[].type`, not on `message`. The `message` string encodes the first error and may change
presentation; the `type` codes will not.

### Seat limit codes

Your organization's parent can enable **seat management** for entity folders. When it is enabled, a
top-level entity folder can carry a seat limit, set from the Lumiform web app. While a limit is in force,
writes that change who can reach that folder are checked against the capacity of the resulting state.

Code | Field | Meaning
---- | ----- | -------
`validation.entityFolderSeatManagement.exceedsChildAllocation` | `seatLimit` | The seat limit is higher than the parent's remaining allocation allows. Lower the limit, or free capacity elsewhere.
`validation.entityFolderSeatManagement.belowChargedUsers` | `seatLimit` | The seat limit is below the number of users already charged to the folder. Raise the limit, or free seats first.
`validation.entityFolderSeatManagement.noFreeSeats` | `users`, or `role` on user writes | The resulting assignments cannot all be charged against the folder's remaining seats. Assign fewer users, or free a seat by removing someone else, or raise the limit in the web app.
`validation.entityFolderSeatManagement.limitedFolderCannotBeNested` | `children` | A folder that carries a seat limit cannot become a child of another folder. Remove the limit in the web app first, then nest it.

> `exceedsChildAllocation`:

```json
{
  "message": "{\"type\":\"validation.entityFolderSeatManagement.exceedsChildAllocation\",\"parameters\":[]}",
  "errors": [
    {
      "type": "validation.entityFolderSeatManagement.exceedsChildAllocation",
      "parameters": [],
      "field": "seatLimit"
    }
  ],
  "code": 422
}
```

> `belowChargedUsers`:

```json
{
  "message": "{\"type\":\"validation.entityFolderSeatManagement.belowChargedUsers\",\"parameters\":[]}",
  "errors": [
    {
      "type": "validation.entityFolderSeatManagement.belowChargedUsers",
      "parameters": [],
      "field": "seatLimit"
    }
  ],
  "code": 422
}
```

> `noFreeSeats`:

```json
{
  "message": "{\"type\":\"validation.entityFolderSeatManagement.noFreeSeats\",\"parameters\":[]}",
  "errors": [
    {
      "type": "validation.entityFolderSeatManagement.noFreeSeats",
      "parameters": [],
      "field": "users"
    }
  ],
  "code": 422
}
```

> `limitedFolderCannotBeNested`:

```json
{
  "message": "{\"type\":\"validation.entityFolderSeatManagement.limitedFolderCannotBeNested\",\"parameters\":[]}",
  "errors": [
    {
      "type": "validation.entityFolderSeatManagement.limitedFolderCannotBeNested",
      "parameters": [],
      "field": "children"
    }
  ],
  "code": 422
}
```

These codes can be returned by write requests on entity folders, entity items, entity types and users.
They are business errors: correct the request before retrying, and do not retry it unchanged.

<aside class="notice">
Seat limits are managed in the Lumiform web app. They are not readable or writable through the Public API,
and no request field of yours is involved -- a request that does not change folder reachability is never
affected. Organizations without seat management enabled never receive these codes.
</aside>
