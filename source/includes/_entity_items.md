# Entity Items

**Note:** If your organization uses seat management, create, update and delete requests on entity items can
fail with `validation.entityFolderSeatManagement.noFreeSeats`, reported on `users` (not guaranteed when the request
changes `entity_folders`; see [Entity Folder Errors](#entity-folder-errors)), when the resulting
assignments exceed the remaining seats of a folder that carries a seat limit. See
[Errors](#validation-errors).

**Note:** Every entity item in a response has two IDs. `id` is the entity item ID used throughout the Public API, including
in URLs and request bodies. `internal_id` is the ID Lumiform uses internally. Use `internal_id` only where Lumiform asks
for an internal ID, for example in entity-prefilled form links. Never send `internal_id` to Public API endpoints.

## Get All Entity Items

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> To include property values in the response, add the `include_properties` query parameter:

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items?include_properties=true' \
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
      "internal_id": 73101,
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
      "internal_id": 73102,
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

This endpoint retrieves all of your entity items. By default, property values are not included in the response. To include them, use the `include_properties=true` query parameter.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-items`

### Response with Properties

When `include_properties=true` is included in the query string, the response will include a `properties` array for each entity item:

> Properties included in response:

```json
{
  "data": [
    {
      "id": 1,
      "internal_id": 73101,
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
      ],
      "properties": [
        {
          "id": 1,
          "entity_type_property_id": 5,
          "value_text": "Some text value",
          "option_values": null
        },
        {
          "id": 2,
          "entity_type_property_id": 6,
          "value_text": null,
          "option_values": [
            {
              "id": 10,
              "label": "Option 1"
            },
            {
              "id": 11,
              "label": "Option 2"
            }
          ]
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/entity-items?page=1&include_properties=true",
    "last": "https://public-api.lumiformapp.com/api/v2/entity-items?page=2&include_properties=true",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/entity-items?page=2&include_properties=true"
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 2,
    "path": "https://public-api.lumiformapp.com/api/v2/entity-items",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

**Properties Field Details:**

- **`id`** - The unique identifier of the property value
- **`entity_type_property_id`** - The ID of the property definition this value belongs to
- **`value_text`** - The text value (for text-type properties). `null` for dropdown properties
- **`option_values`** - Array of selected option values (for dropdown-type properties). `null` or omitted for text properties. Each option value contains:
  - **`id`** - The unique identifier of the option value
  - **`label`** - The display label of the option

### Query Parameters

| Parameter  | Required | Item | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| page       | No | Number | 1 | The results page number to view. If omitted, the default is 1. |
| users      | No | Array | 1,2,3 | A list of user Ids, or a single Id                             |
| entityType | No | Number | 1 | Single Entity Type Id                                          |
| title      | No | Text | warehouse | A string of text to try and find in the entity items titles.   |
| include_properties | No | Boolean | true | When set to `true`, includes property values for each entity item. Defaults to `false`. |

## Get a Specific Entity Item

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> To include property values in the response, add the `include_properties` query parameter:

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1?include_properties=true' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 1,
    "internal_id": 73101,
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
    ],
    "entity_folders": [
      {
        "id": 3,
        "title": "Safety folder"
      }
    ]
  }
}
```

> When `include_properties=true` is included, the response will also contain a `properties` array:

```json
{
  "data": {
    "id": 1,
    "internal_id": 73101,
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
    ],
    "entity_folders": [
      {
        "id": 3,
        "title": "Safety folder"
      }
    ],
    "properties": [
      {
        "id": 1,
        "entity_type_property_id": 5,
        "value_text": "Some text value",
        "option_values": null
      },
      {
        "id": 2,
        "entity_type_property_id": 6,
        "value_text": null,
        "option_values": [
          {
            "id": 10,
            "label": "Option 1"
          },
          {
            "id": 11,
            "label": "Option 2"
          }
        ]
      }
    ]
  }
}
```

This endpoint retrieves a specific Entity Item. By default, property values are not included in the response. To include them, use the `include_properties=true` query parameter.

The response includes `entity_folders`, the entity folders this entity item is in. Each folder has its `id` and `title`. Deleted folders are not listed. `entity_folders` is returned only by this endpoint, not by [Get All Entity Items](#get-all-entity-items).

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/entity-items/<EntityItemId>`

### URL Parameters

| Parameter       | Required | Item | Example | Description |
|-----------------| ------- | ---- | ------- | ----------- |
| EntityItemId  | Yes | Number | 1 | The Id of the entity item to retrieve. |

### Query Parameters

| Parameter  | Required | Item | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| include_properties | No | Boolean | true | When set to `true`, includes property values for the entity item. Defaults to `false`. |

## Create an Entity Item

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","users":[1],"entity_type_id":1}'
```

> To create an entity item with property values, include the `properties` array:

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","users":[1],"entity_type_id":1,"properties":[{"entityTypePropertyId":5,"valueText":"Some text value"},{"entityTypePropertyId":6,"optionValueIds":[10,11]}]}'
```

> To create an entity item in entity folders, include the `entity_folders` array:

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","users":[1],"entity_type_id":1,"entity_folders":[3,4]}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "internal_id": 73101
}
```

This endpoint creates an Entity Item.

If you leave out `entity_folders`, or send an empty list (`[]`) or `null`, the entity item is not put in any folder.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/entity-items`

### Request Body Parameters

| Parameter  | Required | Item | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| title | Yes | String | "Tatooine" | The title of the entity item. |
| description | No | String | "Some description" | The description of the entity item. |
| entity_type_id | Yes | Number | 1 | The ID of the entity type this item belongs to. |
| users | No | Array | [1, 2, 3] | Array of user IDs assigned to this entity item. |
| entity_folders | No | Array | [3, 4] | Array of entity folder IDs to put this entity item in. Use the `id` returned by the [Entity Folders](#entity-folders) endpoints. Can be `null`. |
| properties | No | Array | See below | Array of property values to set for this entity item. |

**Properties Array Structure:**

Each property object in the `properties` array should contain:

| Parameter  | Required | Item | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| entityTypePropertyId | Yes* | Number | 5 | The ID of the entity type property. Required when `properties` array is provided. |
| valueText | No | String | "Some text value" | The text value for text-type properties. Use this for properties with `data_type: "text"`. |
| optionValueIds | No | Array | [10, 11] | Array of option value IDs for dropdown-type properties. Use this for properties with `data_type: "dropdown"`. |

**Note:** For text properties, provide `valueText`. For dropdown properties, provide `optionValueIds`. You should not provide both for the same property.

### Entity Folder Errors

A create or update request fails with a `422` when `entity_folders`:

- contains an ID of a folder that does not exist, belongs to another organization, or has been deleted;
- contains the same ID more than once;
- would put the entity item in a folder whose seat limit is reached (only when your organization uses seat management).

The field these errors are reported on is not guaranteed. Do not rely on it; correct `entity_folders` before retrying.

If `entity_folders` is not an array, or one of its elements is not a number, the request fails with a `422` for `entity_folders`.

## Update an Entity Item

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","users":[1],"entity_type_id":1}'
```

> To update an entity item with property values, include the `properties` array:

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","users":[1],"entity_type_id":1,"properties":[{"entityTypePropertyId":5,"valueText":"Updated text value"},{"entityTypePropertyId":6,"optionValueIds":[10,11]}]}'
```

> To change the entity folders of an entity item, include the `entity_folders` array:

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Tatooine","description":"Some description","entity_type_id":1,"entity_folders":[3,4]}'
```

> The above command does not return any data

This endpoint updates a specific Entity Item.

If you leave out `users`, the assigned users are not changed. Send an empty list (`[]`) or `null` to remove all.

If you leave out `entity_folders`, the entity item's folders are not changed. Send a list of folder IDs to replace them, or an empty list (`[]`) or `null` to remove the entity item from all folders. See [Entity Folder Errors](#entity-folder-errors) for the errors this field can return.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/entity-items/<EntityItemId>`

### URL Parameters

| Parameter      | Required | Item   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityItemId | Yes      | Number | 1       | The Id of the Entity Item to update. |

### Request Body Parameters

| Parameter  | Required | Item | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| title | Yes | String | "Tatooine" | The title of the entity item. |
| description | No | String | "Some description" | The description of the entity item. |
| entity_type_id | Yes | Number | 1 | The ID of the entity type this item belongs to. |
| users | No | Array | [1, 2, 3] | Array of user IDs assigned to this entity item. |
| entity_folders | No | Array | [3, 4] | Array of entity folder IDs this entity item is in. Replaces the current folders. Use the `id` returned by the [Entity Folders](#entity-folders) endpoints. Can be `null`. |
| properties | No | Array | See below | Array of property values to set for this entity item. |

**Properties Array Structure:**

Each property object in the `properties` array should contain:

| Parameter  | Required | Item | Example | Description                                                    |
|------------| ------- | ---- | ------ |----------------------------------------------------------------|
| entityTypePropertyId | Yes* | Number | 5 | The ID of the entity type property. Required when `properties` array is provided. |
| valueText | No | String | "Updated text value" | The text value for text-type properties. Use this for properties with `data_type: "text"`. |
| optionValueIds | No | Array | [10, 11] | Array of option value IDs for dropdown-type properties. Use this for properties with `data_type: "dropdown"`. |

**Note:** For text properties, provide `valueText`. For dropdown properties, provide `optionValueIds`. You should not provide both for the same property.

## Delete an Entity Item

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/entity-items/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> The above command does not return any data

This endpoint deletes a specific Entity Item.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/entity-items/<EntityItemId>`

### URL Parameters

| Parameter      | Required | Item   | Example | Description                            |
|----------------|----------|--------|---------|----------------------------------------|
| EntityItemId | Yes      | Number | 1       | The Id of the Entity Item to delete. |
