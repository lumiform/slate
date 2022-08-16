# Actions

## Get All Actions

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/actions' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
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
      "resolved_by": null,
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
      "resolved_by": null,
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
    "first": "https://public-api.lumiformapp.com/api/v2/actions?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/actions?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/actions?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/actions?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/actions?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/actions?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/actions",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your actions.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/actions`

### Query Parameters

| Parameter     | Required | Type      | Example          | Description                                                                                                                   |
|---------------|----------|-----------|------------------|-------------------------------------------------------------------------------------------------------------------------------|
| page          | No       | Number    | 1                | The results page number to view. If omitted, the default is 1.                                                                |
| resolved_by   | No       | Number    | 1                | The user ID to find actions they have resolved.                                                                               |
| title         | No       | Text      | Check            | A string of text to try and find in the actions titles.                                                                       |
| updated_from  | No       | Unix time | 1585589759       | The date from which to search for the update date of your action.                                                             |
| updated_to    | No       | Unix time | 1630185200       | The date to which to search for the update date of your actions.                                                              |
| created_from  | No       | Unix time | 1585589759       | The date from which to search for the creation date of your actions.                                                          |
| created_to    | No       | Unix time | 1630185200       | The date to which to search for the creation date of your actions.                                                            |
| sites         | No       | Array     | 1,2,3            | A list of site IDs, or a single ID, to search for actions related to them.                                                    |
| resolved_from | No       | Unix time | 1585589759       | The date from which to search for the resolution date of your actions.                                                        |
| resolved_to   | No       | Unix time | 1630185200       | The date to which to search for the resolution date of your actions.                                                          |
| assignees     | No       | Array     | 1,2,3            | A list of user IDs, or a single ID, to search for actions they are assigned to.                                               |
| statuses      | No       | Array     | open,in_progress | A list of statuses, or a single status, to search actions in. **Allowed values:** *open*, *solved*, *in_progress*, *cant_do*. |
| due_from      | No       | Unix time | 1585589759       | The date from which to search for the due date of your actions.                                                               |
| due_to        | No       | Unix time | 1630185200       | The date to which to search for the due date of your actions.                                                                 |
| overdue       | No       | Boolean   | true             | Toggle filtering for overdue or not overdue actions.                                                                          |
| priorities    | No       | Array     | normal           | A list of priorities, or a single priority, to search actions with. **Allowed values:** *normal*, *high*.                     |
| created_by    | No       | Number    | 1                | The user ID to find actions they have created.                                                                                |

<aside class="success">
Tip — the <i>title</i> field is somewhat permissive, so you can try fuzzy matching an action's title!
</aside>

## Get a Specific Action

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/actions/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
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
    "resolved_by": null,
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

This endpoint retrieves a specific action.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/actions/<ActionId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                       |
|-----------|----------|--------|---------|-----------------------------------|
| ActionId  | Yes      | Number | 1       | The ID of the action to retrieve. |
