# Filters
<aside class="success">
Tip — use these endpoints to help you filter resources!
</aside>

## Get All Users
<aside class="warning">
User v1 endpoint is deprecated and will be discontinued in the future. Please refer to v2 documentation bellow.
</aside>

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/filters/users' \
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
      "name": "Obi-Wan Kenobi",
      "email": "obi.wan@jediknights.com"
    },
    {
      "id": 2,
      "name": "Yoda",
      "email": "yoda@jediknights.com"
    },
    {
      "id": 3,
      "name": "Mace Windu",
      "email": "mace.windu@jediknights.com"
    },
    {
      "id": 4,
      "name": "Jocasta Nu",
      "email": "jocasta.nu@jediknights.com"
    },
    {
      "id": 5,
      "name": "Ki-Adi-Mundi",
      "email": "ki.adi.mundi@jediknights.com"
    }
  ]
}
```

This endpoint retrieves all users of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/filters/users`

## Get All Users

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/filters/users' \
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
      "name": "Obi-Wan Kenobi",
      "email": "obi.wan@jediknights.com"
    },
    {
      "id": 2,
      "name": "Yoda",
      "email": "yoda@jediknights.com"
    },
    {
      "id": 3,
      "name": "Mace Windu",
      "email": "mace.windu@jediknights.com"
    },
    {
      "id": 4,
      "name": "Jocasta Nu",
      "email": "jocasta.nu@jediknights.com"
    },
    {
      "id": 5,
      "name": "Ki-Adi-Mundi",
      "email": "ki.adi.mundi@jediknights.com"
    }
  ],
  "links": {
    "first": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/users?page=1",
    "last": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/users?page=1",
    "prev": null,
    "next": null
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/users?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": null,
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/users",
    "per_page": 15,
    "to": 1,
    "total": 1
  }
}
```

This endpoint retrieves all users of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/filters/users`

### Query Parameters

| Parameter | Required | Type   | Example                    | Description                                                    |
|-----------|----------|--------|----------------------------|----------------------------------------------------------------|
| page      | No       | Number | 1                          | The results page number to view. If omitted, the default is 1. |
| name      | No       | Text   | yoda                       | A string of text to try and find in the users names.           |
| email     | No       | Text   | jocasta.nu@jediknights.com | A string of text to try and find in the users e-mails.         |

## Get All Sites
<aside class="warning">
Site v1 endpoint is deprecated and will be discontinued in the future. Please refer to v2 documentation bellow.
</aside>

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/filters/sites' \
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
      "title": "Temple of Coruscant"
    },
    {
      "id": 2,
      "title": "Temple of Ahch-To"
    }
  ]
}
```

This endpoint retrieves all sites of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/filters/sites`

## Get All Sites

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/filters/sites' \
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
      "title": "Temple of Coruscant"
    },
    {
      "id": 2,
      "title": "Temple of Ahch-To"
    }
  ],
  "links": {
    "first": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/sites?page=1",
    "last": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/sites?page=1",
    "prev": null,
    "next": null
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/sites?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": null,
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https:\/\/public-api.lumiformapp.com\/api\/v2\/filters\/sites",
    "per_page": 15,
    "to": 2,
    "total": 2
  }
}
```

This endpoint retrieves all sites of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/filters/sites`

### Query Parameters

| Parameter | Required | Type   | Example | Description                                                    |
|-----------|----------|--------|---------|----------------------------------------------------------------|
| page      | No       | Number | 1       | The results page number to view. If omitted, the default is 1. |
| title     | No       | Text   | berlin  | A string of text to try and find in the sites titles.          |

## Get All Form Templates

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/filters/form-templates' \
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
      "title": "Safety form template",
      "status": "active"
    },
    {
      "id": 2,
      "title": "Materials form template",
      "status": "active"
    },
    {
      "id": 3,
      "title": "Kaminoan cloning tank form template",
      "status": "inactive"
    }
  ]
}
```

This endpoint retrieves all form templates of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/filters/form-templates`


## Get All Checklists
<aside class="warning">
Inspection endpoints are deprecated and will be discontinued in the future. Please refer to Forms and Actions documentation.
</aside>


```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/filters/checklists' \
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
      "status": "active"
    },
    {
      "id": 2,
      "title": "Materials checklist",
      "status": "active"
    },
    {
      "id": 3,
      "title": "Kaminoan cloning tank checklist",
      "status": "inactive"
    }
  ]
}
```

This endpoint retrieves all checklists of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/filters/checklists`
