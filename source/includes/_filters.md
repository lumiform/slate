# Filters
<aside class="success">
Tip — use these endpoints to help you filter resources!
</aside>

## Get All Users

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/filters/users' \
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
      "name": "Obi-Wan Kenobi",
      "email": "obi.wan@jediknights.com"
    },
    {
      "id": 2,
      "name": "Yoda",
      "email": "yoda@jediknights.com"
    },
    {
      "id": 3,
      "name": "Mace Windu",
      "email": "mace.windu@jediknights.com"
    },
    {
      "id": 4,
      "name": "Jocasta Nu",
      "email": "jocasta.nu@jediknights.com"
    },
    {
      "id": 5,
      "name": "Ki-Adi-Mundi",
      "email": "ki.adi.mundi@jediknights.com"
    }
  ]
}
```

This endpoint retrieves all users of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/filters/users`

## Get All Sites

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/filters/sites' \
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
      "title": "Temple of Coruscant"
    },
    {
      "id": 2,
      "title": "Temple of Ahch-To"
    }
  ]
}
```

This endpoint retrieves all sites of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/filters/sites`


## Get All Form Templates

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/filters/form-templates' \
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
      "title": "Safety form template",
      "status": "active"
    },
    {
      "id": 2,
      "title": "Materials form template",
      "status": "active"
    },
    {
      "id": 3,
      "title": "Kaminoan cloning tank form template",
      "status": "inactive"
    }
  ]
}
```

This endpoint retrieves all form templates of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/filters/form-templates`


## Get All Checklists
<aside class="warning">
Inspection endpoints are deprecated and will be discontinued in the future. Please refer to Forms and Actions documentation.
</aside>


```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v1/filters/checklists' \
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
      "status": "active"
    },
    {
      "id": 2,
      "title": "Materials checklist",
      "status": "active"
    },
    {
      "id": 3,
      "title": "Kaminoan cloning tank checklist",
      "status": "inactive"
    }
  ]
}
```

This endpoint retrieves all checklists of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/filters/checklists`
