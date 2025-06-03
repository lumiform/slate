# Forms

## Get All Forms


```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/forms' \
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
      "inspection_title": "Safety checklist",
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
      "issues": [],
      "checklist": {
        "id": 1,
        "title": "Safety checklist",
        "status": "active"
      }
    },
    {
      "id": 2,
      "title": "Lightsaber practice room materials checklist",
      "inspection_title": "Safety checklist",
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
      ],
      "checklist": {
        "id": 2,
        "title": "Materials checklist",
        "status": "active"
      }
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/forms?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/forms?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/forms?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/forms?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/forms?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/forms?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/forms",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your forms.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/forms`

### Query Parameters

Parameter | Required | Type | Example    | Description
--------- | ------- | ---- |------------| -----------
page | No | Number | 1          | The results page number to view. If omitted, the default is 1.
conducted_from | No | Unix time | 1585589759 | The date from which to search for conducted forms.
conducted_to | No | Unix time | 1630185200 | The date to which to search for conducted forms.
due_from | No | Unix time | 1585589759 | The date from which to search for the due date of your forms.
due_to | No | Unix time | 1630185200 | The date to which to search for the due date of your forms.
users | No | Array | 1,2,3      | A list of user IDs, or a single ID, to search for forms they conducted.
sites | No | Array | 1,2,3      | A list of site IDs, or a single ID, to search for forms where they were conducted.
statuses | No | Array | open,taken | A list of statuses, or a single status, to search forms in. **Allowed values:** *open*, *taken*, *closed*, *cant_do*.
overdue | No | Boolean | true       | Toggle filtering for overdue or not overdue forms.
title | No | Text | warehouse  | A string of text to try and find in the forms titles.
checklist | No | Number | 1          | The ID of a checklist to search its conducted forms.
order_by | No | Text | id         | The field to order the results by. **Allowed values:** *id*, *conducted_at*.
order_way | No | Text | ASC         | The field to order the results by. **Allowed values:** *ASC*, *DESC*.

<aside class="success">
Tip — you can combine <i>x_from</i> and <i>x_to</i> parameters to refine your search to a certain time period!
</aside>

## Get a Specific Form

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/forms/1' \
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
    "inspection_title": "Safety checklist",
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
    "issues": [],
    "checklist": {
      "id": 1,
      "title": "Safety checklist",
      "status": "active"
    },
    "photos": [
      {
        "id": "d0ada570-c2db-4cc7-bb29-c18b6d1fef8e.jpeg",
        "url": "https://assets.lumiformapp.com/image-public/d0ada570-c2db-4cc7-bb29-c18b6d1fef8e.jpeg?token=[your token here]",
        "width": null,
        "height": null
      }
    ],
    "approval": {
      "id": 29,
      "status": "approved",
      "comment": null,
      "approver": {
        "id": 4,
        "name": "Jeff Hanneman",
        "email": "jeff.hanneman@slayer.net",
        "admin": 1
      },
      "updated_at": 1748878859
    }
  }
}
```

This endpoint retrieves a specific form.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/forms/<FormId>`

### URL Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
FormId | Yes | Number | 1 | The ID of the form to retrieve.

## Get Questions of a Form

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/forms/1/questions' \
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
      "type": "list",
      "response": "No",
      "max_score": 1,
      "score": 0,
      "percentage": 0,
      "is_negative": true,
      "notes": "Planet Kamino is missing from the archives.",
      "photos": [
        {
          "id": "d0ada570-c2db-4cc7-bb29-c18b6d1fef8e.jpeg",
          "url": "https://assets.lumiformapp.com/image-public/d0ada570-c2db-4cc7-bb29-c18b6d1fef8e.jpeg?token=[your token here]",
          "width": 800,
          "height": 802
        }
      ],
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
      "photos": [],
      "issues": []
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/forms/1/questions?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/forms/1/questions?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/forms/1/questions?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/forms/1/questions?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/forms/1/questions?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/forms/1/questions?page=2",
        "label": "Next »",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/forms/1/questions",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves questions of a specific form.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/forms/<FormId>/questions`

### URL Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
FormId | Yes | Number | 1 | The ID of the form to retrieve questions from.

### Query Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
conducted_from | No | Unix time | 1585589759 | The date from which to search for answered questions.
conducted_to | No | Unix time | 1630185200 | The date to which to search for answered questions.
title | No | Text | archives | A string of text to try and find in the question titles.
response | No | Text | No | A string of text to try and find in the question response.
negative | No | Boolean | true | Toggle filtering for negatively answered questions.

## Export a Specific Form to desired format

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/forms/1/export?format=pdf&timezone=Europe/Berlin' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": "<base64-encoded-string>",
  "format": "pdf"
}
```

This endpoint retrieves a report, encoded in base64 string, for specific form.

### CSV Export caveats

CSV export contains direct links to photos however they are unauthorized for download. To download photos, you need to append query parameter with your token. The final URL should look like: `https://assets.lumiformapp.com/image-public/d0ada570-c2db-4cc7-bb29-c18b6d1fef8e.jpeg?token=[your token here]`

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/forms/<FormId>/export`

### URL Parameters

Parameter | Required | Type | Example | Description
--------- | ------- | ---- | ------- | -----------
FormId | Yes | Number | 1 | The ID of the form to retrieve.

### Query Parameters

Parameter | Required | Type     | Example       | Description
--------- |----------|----------|---------------| -----------
format    | yes      | Text     | pdf           | Format for export. Supported formats: pdf|docx|csv|xlsx
timezone  | yes      | Timezone | Europe/Berlin | Timezone to be used for exporting dates.

