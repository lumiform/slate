# Entity Type Response Sets

## Get All Entity Type Response Sets

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> To include option values in the response, add the `include_option_values` query parameter:

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets?include_option_values=true' \
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
      "name": "Priority Levels"
    },
    {
      "id": 2,
      "name": "Status Options"
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/response-sets?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/response-sets?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/response-sets?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/response-sets?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/response-sets?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/response-sets?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/response-sets",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your entity type response sets. By default, option values are not included in the response. To include them, use the `include_option_values=true` query parameter.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/response-sets`

### Response with Option Values

When `include_option_values=true` is included in the query string, the response will include an `option_values` array for each entity type response set:

> Option values included in response:

```json
{
  "data": [
    {
      "id": 1,
      "name": "Priority Levels",
      "option_values": [
        {
          "id": 1,
          "label": "High"
        },
        {
          "id": 2,
          "label": "Medium"
        },
        {
          "id": 3,
          "label": "Low"
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/response-sets?page=1&include_option_values=true",
    "last": "https://public-api.lumiformapp.com/api/v2/response-sets?page=2&include_option_values=true",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/response-sets?page=2&include_option_values=true"
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 2,
    "path": "https://public-api.lumiformapp.com/api/v2/response-sets",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

**Option Values Field Details:**

- **`id`** - The unique identifier of the option value
- **`label`** - The display label of the option value

### Query Parameters

| Parameter   | Required | Type | Example | Description |
|-------------| ------- | ---- | ------- | ----------- |
| page        | No | Number | 1 | The results page number to view. If omitted, the default is 1. |
| name        | No | Text | priority | A string of text to try and find in the entity type response set names. |
| include_option_values | No | Boolean | true | When set to `true`, includes option values for each entity type response set. Defaults to `false`. |

## Get a Specific Entity Type Response Set

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 1,
    "name": "Priority Levels",
    "option_values": [
      {
        "id": 1,
        "label": "High"
      },
      {
        "id": 2,
        "label": "Medium"
      },
      {
        "id": 3,
        "label": "Low"
      }
    ]
  }
}
```

This endpoint retrieves a specific Entity Type Response Set with its option values.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/response-sets/<ResponseSetId>`

### URL Parameters

| Parameter       | Required | Type | Example | Description |
|-----------------| ------- | ---- | ------- | ----------- |
| ResponseSetId  | Yes | Number | 1 | The Id of the entity type response set to retrieve. |

## Create an Entity Type Response Set

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"name":"Priority Levels"}'
```

> To create an entity type response set with option values, include the `optionValues` array:

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{
    "name": "Priority Levels",
    "optionValues": [
      {
        "label": "High",
        "value": "high",
        "isActive": true
      },
      {
        "label": "Medium",
        "value": "medium",
        "isActive": true
      },
      {
        "label": "Low",
        "value": "low",
        "isActive": true
      }
    ]
  }'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1
}
```

This endpoint creates an Entity Type Response Set.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/response-sets`

### Request Body Parameters

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| name | Yes | String | "Priority Levels" | The name of the entity type response set. Must be unique within your organization. |
| optionValues | No | Array | See below | Array of option values to create for this entity type response set. |

**Option Values Array Structure:**

Each option value object in the `optionValues` array should contain:

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| label | Yes* | String | "High" | The display label of the option value. Required when `optionValues` array is provided. |
| value | No | String | "high" | The value of the option. Can be null. |
| isActive | No | Boolean | true | Whether the option value is active. Defaults to `true`. |

**Note:** The `name` field must be unique within your organization. If an entity type response set with the same name already exists, the request will fail with a validation error.

## Update an Entity Type Response Set

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"name":"Priority Levels Updated"}'
```

> To update an entity type response set with option values, include the `optionValues` array:

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{
    "name": "Priority Levels Updated",
    "optionValues": [
      {
        "id": 1,
        "label": "High Updated",
        "value": "high",
        "isActive": true
      },
      {
        "label": "New Option",
        "value": "new",
        "isActive": true
      }
    ]
  }'
```

> The above command does not return any data

This endpoint updates a specific Entity Type Response Set. When updating option values, existing values not included in the request will be deleted.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/response-sets/<ResponseSetId>`

### URL Parameters

| Parameter      | Required | Type   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| ResponseSetId | Yes      | Number | 1       | The Id of the Entity Type Response Set to update. |

### Request Body Parameters

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| name | Yes | String | "Priority Levels Updated" | The name of the entity type response set. Must be unique within your organization. |
| optionValues | No | Array | See below | Array of option values to update or create for this entity type response set. |

**Option Values Array Structure:**

Each option value object in the `optionValues` array should contain:

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| id | No | Number | 1 | The ID of an existing option value to update. Omit to create a new option value. |
| label | Yes* | String | "High Updated" | The display label of the option value. Required when `optionValues` array is provided. |
| value | No | String | "high" | The value of the option. Can be null. |
| isActive | No | Boolean | true | Whether the option value is active. |

**Note:** The `name` field must be unique within your organization. Include `id` to update an existing option value, or omit it to create a new option value. Existing option values not included in the `optionValues` array will be deleted.

## Delete an Entity Type Response Set

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/response-sets/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> The above command does not return any data

This endpoint deletes a specific Entity Type Response Set. Note that you cannot delete an entity type response set if it is being used by any entity type properties.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/response-sets/<ResponseSetId>`

### URL Parameters

| Parameter      | Required | Type   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| ResponseSetId | Yes      | Number | 1       | The Id of the Entity Type Response Set to delete. |

