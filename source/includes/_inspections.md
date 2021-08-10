# Inspections

## Get All Inspections


```shell
curl --request GET \
  --url 'https://public-api.lumiform.com/api/v1/inspections' \
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
      "title": "Safety checklist",
      "assignees": [
        {
          "id": 1,
          "name": "Obi-Wan Kenobi",
          "email": "obi.wan@jediknights.com"
        },
        {
          "id": 2,
          "name": "Yoda",
          "email": "yoda@jediknights.com"
        }
      ],
      "conducted_by": {
        "id": 1,
        "name": "Obi-Wan Kenobi",
        "email": "obi.wan@jediknights.com"
      },
      "site": {
        "id": 1,
        "title": "Temple of Coruscant"
      },
      "conducted_at": 1585553421,
      "status": "closed",
      "due_at": 1625050211,
      "overdue": false,
      "issues": []
    },
    {
      "id": 2,
      "title": "Lightsaber practice room materials checklist",
      "assignees": [
        {
          "id": 2,
          "name": "Yoda",
          "email": "yoda@jediknights.com"
        }
      ],
      "conducted_by": {
        "id": 2,
        "name": "Yoda",
        "email": "yoda@jediknights.com"
      },
      "site": {
        "id": 1,
        "title": "Temple of Coruscant"
      },
      "conducted_at": 1585589759,
      "status": "closed",
      "due_at": 1595599783,
      "overdue": false,
      "issues": [
        {
          "id": 1,
          "title": "Missing blinding helmets",
          "updated_at": 1593378800,
          "site": {
            "id": 1,
            "title": "Temple of Coruscant"
          },
          "resolved_at": null,
          "resolved_by": null,
          "created_at": 1585589759,
          "assignees": [
            {
              "id": 3,
              "name": "Mace Windu",
              "email": "mace.windu@jediknights.com"
            }
          ],
          "status": "in_progress",
          "due_at": 1630185200,
          "overdue": false,
          "priority": "high",
          "created_by": {
            "id": 2,
            "name": "Yoda",
            "email": "yoda@jediknights.com"
          }
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiform.com/api/v1/inspections?page=1",
    "last": "https://public-api.lumiform.com/api/v1/inspections?page=2",
    "prev": null,
    "next": "https://public-api.lumiform.com/api/v1/inspections?page=2"
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
        "url": "https://public-api.lumiform.com/api/v1/inspections?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiform.com/api/v1/inspections?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiform.com/api/v1/inspections?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiform.com/api/v1/inspections",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your inspections.

### HTTP Request

`GET https://public-api.lumiform.com/api/v1/inspections`

### Query Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
page | No | Number | 1 | The results page number to view. If omitted, the default is 1.
conducted_from | No | Unix time | 1585589759 | The date from which to search for conducted inspections.
conducted_to | No | Unix time | 1630185200 | The date to which to search for conducted inspections.
due_from | No | Unix time | 1585589759 | The date from which to search for the due date of your inspections.
due_to | No | Unix time | 1630185200 | The date to which to search for the due date of your inspections.
users | No | Array | 1,2,3 | A list of user IDs, or a single ID, to search for inspections they conducted.
sites | No | Array | 1,2,3 | A list of site IDs, or a single ID, to search for inspections where they were conducted.
statuses | No | Array | open,taken | A list of statuses, or a single status, to search inspections in. **Allowed values:** *open*, *taken*, *closed*, *cant_do*.
overdue | No | Boolean | true | Toggle filtering for overdue or not overdue inspections.
title | No | Text | warehouse | A string of text to try and find in the inspections titles.

<aside class="success">
Tip — you can combine <i>x_from</i> and <i>x_to</i> parameters to refine your search to a certain time period!
</aside>

## Get a Specific Inspection

```shell
curl --request GET \
  --url 'https://public-api.lumiform.com/api/v1/inspections/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 1,
    "title": "Safety checklist",
    "assignees": [
      {
        "id": 1,
        "name": "Obi-Wan Kenobi",
        "email": "obi.wan@jediknights.com"
      },
      {
        "id": 2,
        "name": "Yoda",
        "email": "yoda@jediknights.com"
      }
    ],
    "conducted_by": {
      "id": 1,
      "name": "Obi-Wan Kenobi",
      "email": "obi.wan@jediknights.com"
    },
    "site": {
      "id": 1,
      "title": "Temple of Coruscant"
    },
    "conducted_at": 1585553421,
    "status": "closed",
    "due_at": 1625050211,
    "overdue": false,
    "issues": []
  }
}
```

This endpoint retrieves a specific inspection.

### HTTP Request

`GET https://public-api.lumiform.com/api/v1/inspections/<InspectionId>`

### URL Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
InspectionId | Yes | Number | 1 | The ID of the inspection to retrieve.

## Get Questions of an Inspection

```shell
curl --request GET \
  --url 'https://public-api.lumiform.com/api/v1/inspections/1/questions' \
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
      "title": "Are the archives complete?",
      "response": "No",
      "max_score": 1,
      "score": 0,
      "percentage": 0,
      "is_negative": true,
      "notes": "Planet Kamino is missing from the archives.",
      "issues": [
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
      ]
    },
    {
      "id": 2,
      "title": "Did the younglings go to bed early?",
      "response": "Yes",
      "max_score": 1,
      "score": 1,
      "percentage": 100,
      "is_negative": false,
      "notes": null,
      "issues": []
    }
  ],
  "links": {
    "first": "https://public-api.lumiform.com/api/v1/inspections/1/questions?page=1",
    "last": "https://public-api.lumiform.com/api/v1/inspections/1/questions?page=2",
    "prev": null,
    "next": "https://public-api.lumiform.com/api/v1/inspections/1/questions?page=2"
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 2,
    "links": [
      {
        "url": null,
        "label": "« Previous",
        "active": false
      },
      {
        "url": "https://public-api.lumiform.com/api/v1/inspections/1/questions?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiform.com/api/v1/inspections/1/questions?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiform.com/api/v1/inspections/1/questions?page=2",
        "label": "Next »",
        "active": false
      }
    ],
    "path": "https://public-api.lumiform.com/api/v1/inspections/1/questions",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves questions of a specific inspection.

### HTTP Request

`GET https://public-api.lumiform.com/api/v1/inspections/<InspectionId>/questions`

### URL Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
InspectionId | Yes | Number | 1 | The ID of the inspection to retrieve questions from.

### Query Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
conducted_from | No | Unix time | 1585589759 | The date from which to search for answered questions.
conducted_to | No | Unix time | 1630185200 | The date to which to search for answered questions.
title | No | Text | archives | A string of text to try and find in the question titles.
response | No | Text | No | A string of text to try and find in the question response.
negative | No | Boolean | true | Toggle filtering for negatively answered questions.

