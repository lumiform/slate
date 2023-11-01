# Groups

## Get All Groups

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/groups' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 868746486,
      "name": "Jedi Order",
      "users": [
        {
          "id": 87913847,
          "name": "Yoda",
          "email": "yoda@jediknights.com"
        }
      ]
    },
    {
      "id": 868746478,
      "name": "Order of the Sith Lords",
      "users": [
        {
          "id": 87913858,
          "name": "Darth Vader",
          "email": "darth.vader@sith.com"
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/groups?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/groups?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/groups?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/groups?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/groups?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/groups?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/groups",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your groups.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/groups`

### Query Parameters

| Parameter | Required | Type      | Example          | Description                                                                    |
|-----------|----------|-----------|------------------|--------------------------------------------------------------------------------|
| name      | No       | Text      | yoda             | A string of text to try and find in the groups names.                          |
| users     | No       | Array     | 1,2,3            | A list of user IDs, or a single ID, to search for groups they are assigned to. |

## Get a Specific Group

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/groups/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "name": "Jedi Order",
    "users": [
      {
        "id": 2,
        "name": "Yoda",
        "email": "yoda@jediknights.com"
      }
    ]
  }
}
```

This endpoint retrieves a specific group.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/groups/<GroupId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                      |
|-----------|----------|--------|---------|----------------------------------|
| GroupId   | Yes      | Number | 1       | The ID of the group to retrieve. |

## Create a Group

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/groups' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"name":"Group name","users":"[1,2]"}'
```

> The above command returns JSON structured like this:

```json
{
  "id": 123
}
```

This endpoint creates a group.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/groups`

## Update a Group

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/groups/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"name":"New group name","users":"[2,3,4]"}'
```

> The above command does not return any data

This endpoint updates a specific group.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/groups/<GroupId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                    |
|-----------|----------|--------|---------|--------------------------------|
| GroupId   | Yes      | Number | 1       | The ID of the group to update. |

## Delete a Group

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/groups/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command does not return any data

This endpoint deletes a specific group.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/groups/<GroupId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                    |
|-----------|----------|--------|---------|--------------------------------|
| GroupId   | Yes      | Number | 1       | The ID of the group to delete. |
