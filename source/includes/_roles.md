# Roles

## Get All Roles

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/roles' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1018907909,
      "name": "Administrator",
      "site_restricted": 0,
      "permissions": [],
      "users": [
        {
          "id": 87913847,
          "name": "Yoda",
          "email": "yoda@jediknights.com",
          "admin": 1
        }
      ],
      "created_at": null,
      "updated_at": null
    },
    {
      "id": 868746486,
      "name": "Sith",
      "site_restricted": false,
      "permissions": [
        "manage-users",
        "manage-sites"        
      ],
      "users": [
        {
          "id": 87913858,
          "name": "Darth Vader",
          "email": "darth.vader@sith.com",
          "admin": 0
        }
      ],
      "created_at": 1588753848,
      "updated_at": 1659609697
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v1/roles?page=1",
    "last": "https://public-api.lumiformapp.com/api/v1/roles?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v1/roles?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v1/roles?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v1/roles?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v1/roles?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v1/roles",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your roles.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/roles`

### Query Parameters

| Parameter       | Required | Type      | Example       | Description                                                                         |
|-----------------|----------|-----------|---------------|-------------------------------------------------------------------------------------|
| site_restricted | No       | Boolean   | false         | A boolean to try and find in the roles that have site restricted.                   |
| users           | No       | Array     | 1,2,3         | A list of user IDs, or a single ID, to search for roles they are assigned to.       |
| permissions     | No       | Array     | role-1,role-2 | A list of permissions, or single permission, to search for roles that contain them. |
| updated_from    | No       | Unix time | 1585589759    | The date from which to search for the update date of your roles.                    |
| updated_to      | No       | Unix time | 1630185200    | The date to which to search for the update date of your roles.                      |
| created_from    | No       | Unix time | 1585589759    | The date from which to search for the creation date of your roles.                  |
| created_to      | No       | Unix time | 1630185200    | The date to which to search for the creation date of your roles.                    |

## Get a Specific Role

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/roles/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 868746486,
    "name": "Sith",
    "site_restricted": false,
    "permissions": [
      "manage-users",
      "manage-sites"
    ],
    "users": [
      {
        "id": 87913858,
        "name": "Darth Vader",
        "email": "darth.vader@sith.com",
        "admin": 0
      }
    ],
    "created_at": 1588753848,
    "updated_at": 1659609697
  }
}
```

This endpoint retrieves a specific role.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/roles/<RoleId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                     |
|-----------|----------|--------|---------|---------------------------------|
| RoleId    | Yes      | Number | 1       | The ID of the role to retrieve. |
