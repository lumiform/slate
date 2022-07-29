# Sites

## Get All Sites

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/sites' \
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
      "name": "Tatooine",
      "description": "It is the home planet of Luke SKywalker",
      "users": [
        {
          "id": 87913847,
          "name": "luke",
          "email": "luke@jediknights.com"
        }
      ],
      "primary_ssid": null,
      "primary_password": null,
      "secondary_ssid": null,
      "secondary_password": null
    },
    {
      "id": 868746478,
      "name": "Alderaan",
      "description": "It is the home planet of Princess Leia Organa",
      "users": [
        {
          "id": 87913858,
          "name": "Leia Organa",
          "email": "leia.organa@sw.com"
        }
      ]
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/sites?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/sites?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/sites?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/sites?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/sites?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/sites?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/sites",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves all of your sites.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/sites`

### Query Parameters

| Parameter | Required | Type  | Example | Description                                                                   |
|-----------|----------|-------|---------|-------------------------------------------------------------------------------|
| title     | No       | Text  | luke    | A string of text to try and find in the sites names.                          |
| users     | No       | Array | 1,2,3   | A list of user IDs, or a single ID, to search for sites they are assigned to. |

## Get a Specific Site

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/sites/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 868746486,
    "name": "Tatooine",
    "description": "It is the home planet of Luke SKywalker",
    "users": [
      {
        "id": 87913847,
        "name": "luke",
        "email": "luke@jediknights.com"
      }
    ],
    "primary_ssid": null,
    "primary_password": null,
    "secondary_ssid": null,
    "secondary_password": null
  }
}
```

This endpoint retrieves a specific site.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/site/<SiteId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                     |
|-----------|----------|--------|---------|---------------------------------|
| SiteId    | Yes      | Number | 1       | The ID of the site to retrieve. |

## Create a Site

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/sites' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"title": "Site name", "description": "site description", "users":"[1,2]"}'
```
> Mandatory fields: title
 
> The above command returns JSON structured like this:

```json
{
  "id": 123
}
```

This endpoint creates a site.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/site`

## Update a Site

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/sites/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --d '{"title": "Site name", "description": "site description", "users":[1,2], "primary_ssid": "123", "primary_password": "123", "secondary_ssid": "123", "secondary_password": "123"}'
```
> Mandatory fields: title

> The above command does not return any data

This endpoint updates a specific site.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/site/<SiteId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                   |
|-----------|----------|--------|---------|-------------------------------|
| SiteId    | Yes      | Number | 1       | The ID of the site to update. |

## Delete a Site

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/sites/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' 
```

> The above command does not return any data

This endpoint deletes a specific site.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/site/<SiteId>`

### URL Parameters

| Parameter | Required | Type   | Example | Description                   |
|-----------|----------|--------|---------|-------------------------------|
| SiteId   | Yes      | Number | 1       | The ID of the site to delete. |
