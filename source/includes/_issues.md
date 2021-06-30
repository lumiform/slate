# Issues

## Get All Issues

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1,
      "title": "Check the droid attack on the Wookies",
      "updated_at": 1593378800,
      "site": {
        "id": 1,
        "title": "Temple of Coruscant"
      },
      "resolved_at": 1624914800,
      "created_at": 1598649200,
      "assignees": [
        {
          "id": 2,
          "name": "Yoda",
          "email": "yoda@jediknights.com"
        }
      ],
      "status": "in_progress",
      "due_at": 1630185200,
      "overdue": false,
      "priority": "normal",
      "created_by": {
        "id": 5,
        "name": "Ki-Adi-Mundi",
        "email": "ki.adi.mundi@jediknights.com"
      }
    },
    {
      "id": 2,
      "title": "Add Kamino to the archives",
      "updated_at": 1593378800,
      "site": {
        "id": 1,
        "title": "Temple of Coruscant"
      },
      "resolved_at": 1624914800,
      "created_at": 1598649200,
      "assignees": [
        {
          "id": 4,
          "name": "Jocasta Nu",
          "email": "jocasta.nu@jediknights.com"
        }
      ],
      "status": "in_progress",
      "due_at": 1630185200,
      "overdue": false,
      "priority": "high",
      "created_by": {
        "id": 1,
        "name": "Obi-Wan Kenobi",
        "email": "obi.wan@jediknights.com"
      }
    }
  ],
  "links": {
    "first": "http://public-api.lumiformdev.com/api/v1/issues?page=1",
    "last": "http://public-api.lumiformdev.com/api/v1/issues?page=2",
    "prev": null,
    "next": "http://public-api.lumiformdev.com/api/v1/issues?page=2"
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 2,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "http://public-api.lumiformdev.com/api/v1/issues?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "http://public-api.lumiformdev.com/api/v1/issues?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "http://public-api.lumiformdev.com/api/v1/issues?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "http://public-api.lumiformdev.com/api/v1/issues",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your issues.

### HTTP Request

`GET http://public-api.lumiformdev.com/api/v1/issues`

### Query Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
page | No | Number | 1 | The results page number to view. If omitted, the default is 1.
resolved_by | No | Number | 1 | The user ID to find issues they have resolved.
title | No | Text | Check | A string of text to try and find in the issues titles.
updated_from | No | Unix time | 1585589759 | The date from which to search for the update date of your issue.
updated_to | No | Unix time | 1630185200 | The date to which to search for the update date of your issues.
created_from | No | Unix time | 1585589759 | The date from which to search for the creation date of your issues.
created_to | No | Unix time | 1630185200 | The date to which to search for the creation date of your issues.
sites | No | Array | 1,2,3 | A list of site IDs, or a single ID, to search for issues related to them.
resolved_from | No | Unix time | 1585589759 | The date from which to search for the resolution date of your issues.
resolved_to | No | Unix time | 1630185200 | The date to which to search for the resolution date of your issues.
assignees | No | Array | 1,2,3 | A list of user IDs, or a single ID, to search for issues they are assigned to.
statuses | No | Array | open,in_progress | A list of statuses, or a single status, to search issues in. **Allowed values:** *open*, *solved*, *in_progress*, *cant_do*.
due_from | No | Unix time | 1585589759 | The date from which to search for the due date of your issues.
due_to | No | Unix time | 1630185200 | The date to which to search for the due date of your issues.
overdue | No | Boolean | true | Toggle filtering for overdue or not overdue issues.
priorities | No | Array | normal | A list of priorities, or a single priority, to search issues with. **Allowed values:** *normal*, *high*.
created_by | No | Number | 1 | The user ID to find issues they have created.

<aside class="success">
Tip — the <i>title</i> field is somewhat permissive, so you can try fuzzy matching an issue's title!
</aside>

## Get a Specific Issue

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 1,
    "title": "Check the droid attack on the Wookies",
    "updated_at": 1593378800,
    "site": {
      "id": 1,
      "title": "Temple of Coruscant"
    },
    "resolved_at": 1624914800,
    "created_at": 1598649200,
    "assignees": [
      {
        "id": 2,
        "name": "Yoda",
        "email": "yoda@jediknights.com"
      }
    ],
    "status": "in_progress",
    "due_at": 1630185200,
    "overdue": false,
    "priority": "normal",
    "created_by": {
      "id": 5,
      "name": "Ki-Adi-Mundi",
      "email": "ki.adi.mundi@jediknights.com"
    }
  }
}
```

This endpoint retrieves a specific issue.

### HTTP Request

`GET http://public-api.lumiformdev.com/api/v1/issues/<IssueId>`

### URL Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
IssueId | Yes | Number | 1 | The ID of the issue to retrieve.
