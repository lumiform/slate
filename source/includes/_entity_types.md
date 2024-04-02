# Entity Types

## Get All Entity Types

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types' \
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
      "description": "This checklist is about safety"
    },
    {
      "id": 2,
      "title": "Cleaning checklist",
      "description": "This checklist is about cleaning facility"
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/entity-types?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/entity-types?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/entity-types?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/entity-types?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/entity-types?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/entity-types?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/entity-types",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your entity types.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-types`

### Query Parameters

| Parameter   | Required | Type | Example | Description |
|-------------| ------- | ---- | ------- | ----------- |
| page        | No | Number | 1 | The results page number to view. If omitted, the default is 1. |
| title       | No | Text | warehouse | A string of text to try and find in the entity types titles. |

## Get a Specific Entity Type

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types/1' \
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
    "description": "This checklist is about safety"
  }
}
```

This endpoint retrieves a specific Entity Type.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-types/<EntityTypeId>`

### URL Parameters

| Parameter       | Required | Type | Example | Description |
|-----------------| ------- | ---- | ------- | ----------- |
| EntityTypeId  | Yes | Number | 1 | The Id of the entity type to retrieve. |

## Create an Entity Type


```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"title":"Tatooine","description":"Some description"}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1
}
```

This endpoint creates an Entity Type.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/entity-types`

## Update an Entity Type

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"title":"Tatooine","description":"Some description"}'
```

> The above command does not return any data

This endpoint updates a specific Entity Type.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/entity-types/<EntityTypeId>`

### URL Parameters

| Parameter      | Required | Type   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityTypeId | Yes      | Number | 1       | The Id of the Entity Type to update. |

## Delete an Entity Type

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command does not return any data

This endpoint deletes a specific Entity Type.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/entity-types/<EntityTypeId>`

### URL Parameters

| Parameter      | Required | Type   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityTypeId | Yes      | Number | 1       | The Id of the Entity Type to delete. |
