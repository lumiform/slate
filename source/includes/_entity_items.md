# Entity Items

## Get All Entity Items

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Item: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1,
      "title": "Safety checklist",
      "description": "This checklist is about safety",
      "entity_type": {
        "id": 1,
        "title": "Safety",
        "description": "Safety related entities"
      },
      "users": [
        {
          "id": 1,
          "name": "John Doe",
          "email": "john.doe@lumiformapp.com",
          "admin": 0
        }
      ]
    },
    {
      "id": 2,
      "title": "Cleaning checklist",
      "description": "This checklist is about cleaning facility",
      "entity_type": {
        "id": 2,
        "title": "Cleaning",
        "description": "Cleaning related entities"
      },
      "users": [
        {
          "id": 1,
          "name": "John Doe",
          "email": "john.doe@lumiformapp.com",
          "admin": 0
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/entity-items?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/entity-items?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/entity-items?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/entity-items?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/entity-items?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/entity-items?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/entity-items",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your entity items.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-items`

### Query Parameters

| Parameter  | Required | Item | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| page       | No | Number | 1 | The results page number to view. If omitted, the default is 1. |
| users      | No | Array | 1,2,3 | A list of user Ids, or a single Id                             |
| entityType | No | Number | 1 | Single Entity Type Id                                          |
| title      | No | Text | warehouse | A string of text to try and find in the entity items titles.   |

## Get a Specific Entity Item

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Item: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 1,
    "title": "Safety checklist",
    "description": "This checklist is about safety",
    "entity_type": {
      "id": 2,
      "title": "Cleaning",
      "description": "Cleaning related entities"
    },
    "users": [
      {
        "id": 1,
        "name": "John Doe",
        "email": "john.doe@lumiformapp.com",
        "admin": 0
      }
    ]
  }
}
```

This endpoint retrieves a specific Entity Item.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-items/<EntityItemId>`

### URL Parameters

| Parameter       | Required | Item | Example | Description |
|-----------------| ------- | ---- | ------- | ----------- |
| EntityItemId  | Yes | Number | 1 | The Id of the entity item to retrieve. |

## Create an Entity Item


```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Item: application/json' \
  --d '{"title":"Tatooine","description":"Some description","users":[1],"entity_type_id":1}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1
}
```

This endpoint creates an Entity Item.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/entity-items`

## Update an Entity Item

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Item: application/json' \
  --d '{"title":"Tatooine","description":"Some description","users":[1],"entity_type_id":1}'
```

> The above command does not return any data

This endpoint updates a specific Entity Item.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/entity-items/<EntityItemId>`

### URL Parameters

| Parameter      | Required | Item   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityItemId | Yes      | Number | 1       | The Id of the Entity Item to update. |

## Delete an Entity Item

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Item: application/json' 
```

> The above command does not return any data

This endpoint deletes a specific Entity Item.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/entity-items/<EntityItemId>`

### URL Parameters

| Parameter      | Required | Item   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityItemId | Yes      | Number | 1       | The Id of the Entity Item to delete. |
