# Filters
<aside class="success">
Tip — use these endpoints to help you filter resources!
</aside>

## Get All Users (v1)
<aside class="warning">
User v1 endpoint is deprecated and will be discontinued in the future. Please refer to v2 documentation.
</aside>

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

## Get All Sites (v1)
<aside class="warning">
Site v1 endpoint is deprecated and will be discontinued in the future. Please refer to v2 documentation.
</aside>

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
      "internal_id": 50231,
      "title": "Safety form template",
      "status": "active"
    },
    {
      "id": 2,
      "internal_id": 50232,
      "title": "Materials form template",
      "status": "active"
    },
    {
      "id": 3,
      "internal_id": 50233,
      "title": "Kaminoan cloning tank form template",
      "status": "inactive"
    }
  ]
}
```

This endpoint retrieves all form templates of your organization.

Each form template has two IDs. `id` is the form template ID used throughout the Public API. `internal_id` is the ID
Lumiform uses internally. Use `internal_id` only where Lumiform asks for an internal ID, for example in entity-prefilled
form links. Never send `internal_id` to Public API endpoints.

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
      "internal_id": 50231,
      "title": "Safety checklist",
      "status": "active"
    },
    {
      "id": 2,
      "internal_id": 50232,
      "title": "Materials checklist",
      "status": "active"
    },
    {
      "id": 3,
      "internal_id": 50233,
      "title": "Kaminoan cloning tank checklist",
      "status": "inactive"
    }
  ]
}
```

This endpoint retrieves all checklists of your organization.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v1/filters/checklists`
