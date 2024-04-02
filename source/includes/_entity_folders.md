# Entity Folders

## Get All Entity Folders

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-folders' \
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
      "title": "Safety folder",
      "parents": [
        {
          "id": 2,
          "title": "Parent folder"
        }
      ],
      "children": [
        {
          "id": 3,
          "title": "Child folder"
        }
      ],
      "users": [
        {
          "id": 1,
          "name": "Obi-Wan Kenobi",
          "email": "obi.wan@jediknights.com",
          "admin": 0
        }
      ],
      "entity_items": [
        {
          "id": 1,
          "title": "Entity item",
          "description": null
        }
      ],
      "labels": [
        {
          "id": 1,
          "label": "Label"
        }
      ]
    },

    {
      "id": 2,
      "title": "Safety folder",
      "parents": [
        {
          "id": 4,
          "title": "Parent folder"
        }
      ],
      "children": [
        {
          "id": 5,
          "title": "Child folder"
        }
      ],
      "users": [
        {
          "id": 1,
          "name": "Obi-Wan Kenobi",
          "email": "obi.wan@jediknights.com",
          "admin": 0
        }
      ],
      "entity_items": [
        {
          "id": 1,
          "title": "Entity item",
          "description": null
        }
      ],
      "labels": [
        {
          "id": 1,
          "label": "Label"
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/entity-folders?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/entity-folders?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/entity-folders?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/entity-folders?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/entity-folders?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/entity-folders?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/entity-folders",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your entity folders.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-folders`

### Query Parameters

| Parameter   | Required | Type | Example | Description |
|-------------| ------- | ---- | ------- | ----------- |
| page        | No | Number | 1 | The results page number to view. If omitted, the default is 1. |
| users       | No | Array | 1,2,3 | A list of user Ids, or a single Id |
| entityItems | No | Array | 1,2,3 | A list of entity items Ids, or a single Id |
| title       | No | Text | warehouse | A string of text to try and find in the entity folders titles. |

## Get a Specific Entity Folder

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-folders/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 1,
    "title": "Safety folder",
    "parents": [
      {
        "id": 2,
        "title": "Parent folder"
      }
    ],
    "children": [
      {
        "id": 3,
        "title": "Child folder"
      }
    ],
    "users": [
      {
        "id": 1,
        "name": "Obi-Wan Kenobi",
        "email": "obi.wan@jediknights.com",
        "admin": 0
      }
    ],
    "entity_items": [
      {
        "id": 1,
        "title": "Entity item",
        "description": null
      }
    ],
    "labels": [
      {
        "id": 1,
        "label": "Label"
      }
    ]
  }
}
```

This endpoint retrieves a specific Entity Folder.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-folders/<EntityFolderId>`

### URL Parameters

| Parameter       | Required | Type | Example | Description |
|-----------------| ------- | ---- | ------- | ----------- |
| EntityFolderId  | Yes | Number | 1 | The Id of the entity folder to retrieve. |

## Create an Entity Folder


```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-folders' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"title":"Tatooine","children":[1],"labels":["Label 1","Label 2"],"entity_items":[1,2,3],"users":[1,2,3]}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1
}
```

This endpoint creates an Entity Folder.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/entity-folders`

## Update an Entity Folder

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-folders/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"title":"Tatooine","children":[1],"labels":["Label 1","Label 2"],"entity_items":[1,2,3],"users":[1,2,3]}'
```

> The above command does not return any data

This endpoint updates a specific Entity Folder.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/entity-folders/<EntityFolderId>`

### URL Parameters

| Parameter      | Required | Type   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityFolderId | Yes      | Number | 1       | The Id of the Entity Folder to update. |

## Delete an Entity Folder

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-folders/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command does not return any data

This endpoint deletes a specific Entity Folder.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/entity-folders/<EntityFolderId>`

### URL Parameters

| Parameter      | Required | Type   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityFolderId | Yes      | Number | 1       | The Id of the Entity Folder to delete. |
