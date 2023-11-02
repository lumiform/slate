# Users

## Get All Users

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/users' \
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
      "name": "Leia Organa",
      "email": "leia.organa@sw.com",
      "role": {
        "id": 1018907909,
        "name": "Administrator"
      },
      "admin": 1
    },
    {
      "id": 868746486,
      "name": "Luke Skywalker",
      "email": "luke@sw.com",
      "role": {
        "id": 576577251,
        "name": "Jedi"
      },
      "admin": 1      
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/users?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/users?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/users?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/users?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/users?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/users?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/users",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your users.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/users`

### Query Parameters

| Parameter | Required | Type | Example     | Description                                           |
|-----------|----------|------|-------------|-------------------------------------------------------|
| name      | No       | Text | luke        | A string of text to try and find in the users names.  |
| email     | No       | Text | luke@sw.com | A string of text to try and find in the users emails. |

## Get a Specific User

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/users/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 868746486,
    "name": "Luke Skywalker",
    "email": "luke@sw.com",
    "role": {
      "id": 576577251,
      "name": "Jedi"
    },
    "admin": 1
  }
}
```

This endpoint retrieves a specific user.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/users/<UserId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                     |
|-----------|----------|--------|---------|---------------------------------|
| UserId    | Yes      | Number | 1       | The ID of the user to retrieve. |

## Create a User

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/users' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"name": "User name", "email": "user@mail.com", "role": 123456}'
```
> Mandatory fields: All
 
> The above command returns JSON structured like this:

```json
{
  "id": 123
}
```

This endpoint creates a user.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/users`

## Update a User

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/users/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"name": "User name", "email": "user@mail.com", "role": 123456}'
```
> Mandatory fields: All

> The above command does not return any data

This endpoint updates a specific user.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/users/<UserId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                   |
|-----------|----------|--------|---------|-------------------------------|
| UserId    | Yes      | Number | 1       | The ID of the user to update. |

## Delete a User

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/users/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command does not return any data

This endpoint deletes a specific user.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/users/<UserId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                   |
|-----------|----------|--------|---------|-------------------------------|
| UserId    | Yes      | Number | 1       | The ID of the user to delete. |
