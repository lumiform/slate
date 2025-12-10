# Entity Types

## Get All Entity Types

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> To include properties in the response, add the `include_properties` query parameter:

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types?include_properties=true' \
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

This endpoint retrieves all of your entity types. By default, properties are not included in the response. To include them, use the `include_properties=true` query parameter.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-types`

### Response with Properties

When `include_properties=true` is included in the query string, the response will include a `properties` array for each entity type:

> Properties included in response:

```json
{
  "data": [
    {
      "id": 1,
      "title": "Safety checklist",
      "description": "This checklist is about safety",
      "properties": [
        {
          "id": 1,
          "label": "Location",
          "data_type": "text",
          "allow_multi": false
        },
        {
          "id": 2,
          "label": "Status",
          "data_type": "dropdown",
          "option_set_id": 1,
          "allow_multi": false,
          "option_values": [
            {
              "id": 1,
              "label": "Active"
            },
            {
              "id": 2,
              "label": "Inactive"
            }
          ]
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/entity-types?page=1&include_properties=true",
    "last": "https://public-api.lumiformapp.com/api/v2/entity-types?page=2&include_properties=true",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/entity-types?page=2&include_properties=true"
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 2,
    "path": "https://public-api.lumiformapp.com/api/v2/entity-types",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

**Properties Field Details:**

- **`id`** - The unique identifier of the property definition
- **`label`** - The display label of the property
- **`data_type`** - The type of property: `"text"` or `"dropdown"`
- **`allow_multi`** - Whether multiple values are allowed for this property
- **`option_set_id`** - The ID of the option set (only present for dropdown-type properties)
- **`option_values`** - Array of available option values (only present for dropdown-type properties). Each option value contains:
  - **`id`** - The unique identifier of the option value
  - **`label`** - The display label of the option

### Query Parameters

| Parameter   | Required | Type | Example | Description |
|-------------| ------- | ---- | ------- | ----------- |
| page        | No | Number | 1 | The results page number to view. If omitted, the default is 1. |
| title       | No | Text | warehouse | A string of text to try and find in the entity types titles. |
| include_properties | No | Boolean | true | When set to `true`, includes property definitions for each entity type. Defaults to `false`. |

## Get a Specific Entity Type

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> To include properties in the response, add the `include_properties` query parameter:

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types/1?include_properties=true' \
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

> When `include_properties=true` is included, the response will also contain a `properties` array:

```json
{
  "data": {
    "id": 1,
    "title": "Safety checklist",
    "description": "This checklist is about safety",
    "properties": [
      {
        "id": 1,
        "label": "Location",
        "data_type": "text",
        "allow_multi": false
      },
      {
        "id": 2,
        "label": "Status",
        "data_type": "dropdown",
        "option_set_id": 1,
        "allow_multi": false,
        "option_values": [
          {
            "id": 1,
            "label": "Active"
          },
          {
            "id": 2,
            "label": "Inactive"
          }
        ]
      }
    ]
  }
}
```

This endpoint retrieves a specific Entity Type. By default, properties are not included in the response. To include them, use the `include_properties=true` query parameter.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-types/<EntityTypeId>`

### URL Parameters

| Parameter       | Required | Type | Example | Description |
|-----------------| ------- | ---- | ------- | ----------- |
| EntityTypeId  | Yes | Number | 1 | The Id of the entity type to retrieve. |

### Query Parameters

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| include_properties | No | Boolean | true | When set to `true`, includes property definitions for the entity type. Defaults to `false`. |

## Create an Entity Type

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description"}'
```

> To create an entity type with property definitions, include the `properties` array:

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","properties":[{"label":"Location","dataType":"text","allowMulti":false},{"label":"Status","dataType":"dropdown","optionSetId":1,"allowMulti":false}]}'
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

### Request Body Parameters

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| title | Yes | String | "Tatooine" | The title of the entity type. |
| description | No | String | "Some description" | The description of the entity type. |
| properties | No | Array | See below | Array of property definitions to create for this entity type. |

**Properties Array Structure:**

Each property object in the `properties` array should contain:

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| label | Yes* | String | "Location" | The display label of the property. Required when `properties` array is provided. |
| dataType | Yes* | String | "text" or "dropdown" | The data type of the property. Must be either `"text"` or `"dropdown"`. Required when `properties` array is provided. |
| optionSetId | No | Number | 1 | The ID of the option set. Required when `dataType` is `"dropdown"`. Not used for `"text"` properties. |
| allowMulti | No | Boolean | false | Whether multiple values are allowed for this property. Defaults to `false`. |

**Note:** For dropdown properties, `optionSetId` is required. For text properties, `optionSetId` should not be provided.

## Update an Entity Type

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description"}'
```

> To update an entity type with property definitions, include the `properties` array:

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-types/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","properties":[{"id":5,"label":"Updated Location","dataType":"text","allowMulti":false},{"label":"New Status","dataType":"dropdown","optionSetId":1,"allowMulti":false}]}'
```

> The above command does not return any data

This endpoint updates a specific Entity Type.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/entity-types/<EntityTypeId>`

### URL Parameters

| Parameter      | Required | Type   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityTypeId | Yes      | Number | 1       | The Id of the Entity Type to update. |

### Request Body Parameters

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| title | Yes | String | "Tatooine" | The title of the entity type. |
| description | No | String | "Some description" | The description of the entity type. |
| properties | No | Array | See below | Array of property definitions to update or create for this entity type. |

**Properties Array Structure:**

Each property object in the `properties` array should contain:

| Parameter  | Required | Type | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| id | No | Number | 5 | The ID of an existing property to update. Omit to create a new property. |
| label | Yes* | String | "Updated Location" | The display label of the property. Required when `properties` array is provided. |
| dataType | Yes* | String | "text" or "dropdown" | The data type of the property. Must be either `"text"` or `"dropdown"`. Required when `properties` array is provided. |
| optionSetId | No | Number | 1 | The ID of the option set. Required when `dataType` is `"dropdown"`. Not used for `"text"` properties. |
| allowMulti | No | Boolean | false | Whether multiple values are allowed for this property. Defaults to `false`. |

**Note:** For dropdown properties, `optionSetId` is required. For text properties, `optionSetId` should not be provided. Include `id` to update an existing property, or omit it to create a new property.

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
