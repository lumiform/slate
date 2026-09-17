# Schedules

Schedules create repeating inspections and todos from form templates.

List and retrieve responses include the stored `rrule` string. Create and update send an editor `rule` object, not that string. To change recurrence, [decode](#decode-an-rrule) the stored `rrule`, edit the returned `rule`, map related resource objects to IDs, and send the complete schedule through [Update a Schedule](#update-a-schedule).

Reads return related form templates, users, groups, and entity items as resource objects. Writes use arrays of those resources' IDs. Retrieved reminders include the derived read-only `time_shift` field. When writing reminders, send `id` where applicable, `type`, `direction`, `scale`, and `value`; `time_shift` does not need to be sent.

`timezone` is an IANA name such as `Europe/Berlin`. Send it on create and update. The Public API resolves it internally. Legacy reads may return `null`. Clients never send or receive a timezone identifier.

Related form templates, users, groups, entity items, and reminders must be accessible to your organization. Invalid or inaccessible IDs return a 422 validation error. A schedule that belongs to another organization cannot be retrieved, updated, or deleted.

All IDs in requests and responses are Public API IDs. `created_at` and `updated_at` are Unix timestamps.

A complete pass against a test organization is: [create](#create-a-schedule) a schedule, [list](#get-all-schedules) it, [retrieve](#get-a-specific-schedule) it, [decode](#decode-an-rrule) its `rrule`, edit the returned `rule`, map related resource objects to IDs, [replace](#update-a-schedule) the schedule, then [delete](#delete-a-schedule) it.

## Get All Schedules

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/schedules' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 739184205,
      "title": "Temple opening",
      "status": "active",
      "due_in": 90,
      "expire_after_days": 7,
      "timezone": "Europe/Berlin",
      "rrule": "DTSTART:20241028T121625Z\nRRULE:FREQ=DAILY",
      "created_at": 1730117785,
      "updated_at": 1730117785
    },
    {
      "id": 739184206,
      "title": "Archive review",
      "status": "inactive",
      "due_in": 60,
      "expire_after_days": null,
      "timezone": null,
      "rrule": "DTSTART:20241028T121625Z\nRRULE:FREQ=YEARLY;COUNT=1",
      "created_at": 1730117785,
      "updated_at": 1730117785
    }
  ],
  "links": {
    "first": "https://public-api.lumiformapp.com/api/v2/schedules?page=1",
    "last": "https://public-api.lumiformapp.com/api/v2/schedules?page=2",
    "prev": null,
    "next": "https://public-api.lumiformapp.com/api/v2/schedules?page=2"
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
        "url": "https://public-api.lumiformapp.com/api/v2/schedules?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/schedules?page=2",
        "label": "2",
        "active": false
      },
      {
        "url": "https://public-api.lumiformapp.com/api/v2/schedules?page=2",
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "https://public-api.lumiformapp.com/api/v2/schedules",
    "per_page": 15,
    "to": 15,
    "total": 30
  }
}
```

This endpoint retrieves the schedules in your organization. Results use the standard paginated `data`, `links`, and `meta` envelope.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/schedules`

### Query Parameters

| Parameter | Required | Type   | Example | Description                                                    |
|-----------|----------|--------|---------|----------------------------------------------------------------|
| page      | No       | Number | 1       | The results page number to view. If omitted, the default is 1. |

### Response Fields

| Field              | Type           | Description                                                                 |
|--------------------|----------------|-----------------------------------------------------------------------------|
| id                 | Number         | The schedule ID.                                                            |
| title              | String or null | The schedule title.                                                         |
| status             | String         | `active` or `inactive`.                                                     |
| due_in             | Number         | Minutes after each occurrence starts until the inspection is due.           |
| expire_after_days  | Number or null | Extra days after each inspection due date before it expires.                |
| timezone           | String or null | IANA timezone name. `null` on some legacy schedules.                        |
| rrule              | String         | The stored recurrence string.                                               |
| created_at         | Number         | Unix timestamp.                                                             |
| updated_at         | Number         | Unix timestamp.                                                             |

## Get a Specific Schedule

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/schedules/739184205' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 739184205,
    "title": "Temple opening",
    "status": "active",
    "due_in": 90,
    "expire_after_days": 7,
    "timezone": "Europe/Berlin",
    "rrule": "DTSTART:20241028T121625Z\nRRULE:FREQ=DAILY",
    "created_at": 1730117785,
    "updated_at": 1730117785,
    "separate_todo_for_all_users": false,
    "entity_item_specific_assignments": false,
    "form_templates": [
      {
        "id": 1018907909,
        "title": "Safety checklist",
        "status": "active"
      }
    ],
    "assignees": {
      "users": [
        {
          "id": 868746486,
          "name": "Obi-Wan Kenobi",
          "email": "obi.wan@jediknights.com",
          "admin": 0
        }
      ],
      "groups": [
        {
          "id": 868746478,
          "name": "Jedi Order"
        }
      ],
      "entity_items": [
        {
          "id": 412578903,
          "title": "Temple of Coruscant",
          "description": null
        }
      ],
      "all_entity_items": false
    },
    "supervisors": {
      "users": [
        {
          "id": 87913847,
          "name": "Yoda",
          "email": "yoda@jediknights.com",
          "admin": 1
        }
      ],
      "groups": []
    },
    "reminders": [
      {
        "id": 576577251,
        "type": "available",
        "direction": "before",
        "scale": "hour",
        "value": 2,
        "time_shift": -120
      }
    ]
  }
}
```

This endpoint retrieves a specific schedule, including related resources and reminders.

Do not send this payload unchanged to update. Map `form_templates`, `assignees`, and `supervisors` resource objects to arrays of IDs. Retrieved reminders include the derived read-only `time_shift` field; when writing, send `id` where applicable, `type`, `direction`, `scale`, and `value`.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/schedules/<ScheduleId>`

### URL Parameters

| Parameter  | Required | Type   | Example   | Description                        |
|------------|----------|--------|-----------|------------------------------------|
| ScheduleId | Yes      | Number | 739184205 | The ID of the schedule to retrieve. |

### Additional Response Fields

Every [index](#get-all-schedules) field, plus:

| Field                              | Type    | Description                                                                                          |
|------------------------------------|---------|------------------------------------------------------------------------------------------------------|
| separate_todo_for_all_users        | Boolean | When `true`, each assignee receives a separate todo and inspection.                                  |
| entity_item_specific_assignments   | Boolean | When `true`, assignments are specific to the selected entity items.                                  |
| form_templates                     | Array   | Form templates on the schedule. Each object has `id`, `title`, and `status`.                         |
| assignees.users                    | Array   | Assigned users (`id`, `name`, `email`, `admin`).                                                     |
| assignees.groups                   | Array   | Assigned groups (`id`, `name`).                                                                      |
| assignees.entity_items             | Array   | Assigned entity items (`id`, `title`, `description`).                                                |
| assignees.all_entity_items         | Boolean | When `true`, the schedule applies to all entity items.                                               |
| supervisors.users                  | Array   | Supervising users (`id`, `name`, `email`, `admin`).                                                  |
| supervisors.groups                 | Array   | Supervising groups (`id`, `name`).                                                                   |
| reminders                          | Array   | Reminders with `id`, `type`, `direction`, `scale`, `value`, and `time_shift`.                        |
| reminders[].time_shift             | Number  | Derived read-only offset in minutes. Negative means before; positive means after. Not a timezone offset. |

A schedule from another organization returns 403. An unknown or deleted schedule returns 404.

## Create a Schedule

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/schedules' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Temple opening","due_in":90,"expire_after_days":7,"separate_todo_for_all_users":false,"entity_item_specific_assignments":false,"timezone":"Europe/Berlin","form_templates":[1018907909],"assignees":{"users":[868746486],"groups":[868746478],"entity_items":[412578903],"all_entity_items":false},"supervisors":{"users":[87913847],"groups":[]},"rule":{"start":1730117785,"repeat":"daily","interval":1},"reminders":[{"type":"available","direction":"before","scale":"hour","value":2}]}'
```

> Request body:

```json
{
  "title": "Temple opening",
  "due_in": 90,
  "expire_after_days": 7,
  "separate_todo_for_all_users": false,
  "entity_item_specific_assignments": false,
  "timezone": "Europe/Berlin",
  "form_templates": [1018907909],
  "assignees": {
    "users": [868746486],
    "groups": [868746478],
    "entity_items": [412578903],
    "all_entity_items": false
  },
  "supervisors": {
    "users": [87913847],
    "groups": []
  },
  "rule": {
    "start": 1730117785,
    "repeat": "daily",
    "interval": 1
  },
  "reminders": [
    {
      "type": "available",
      "direction": "before",
      "scale": "hour",
      "value": 2
    }
  ]
}
```

> The above command returns JSON structured like this:

```json
{
  "id": 739184205
}
```

This endpoint creates a schedule. Send `form_templates` and `reminders` even when they are empty arrays. Do not send `rrule` or `status`. Do not send reminder `id` on create.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/schedules`

### Request Body Parameters

| Parameter                            | Required | Type            | Example         | Description                                                                 |
|--------------------------------------|----------|-----------------|-----------------|-----------------------------------------------------------------------------|
| title                                | No       | String or null  | "Temple opening"| The schedule title.                                                         |
| due_in                               | Yes      | Number          | 90              | Integer number of minutes after each occurrence starts until the inspection is due. Must be `>= 0`. |
| expire_after_days                    | No       | Number or null  | 7               | Extra days after each inspection due date before it expires. `0`–`365`.     |
| separate_todo_for_all_users          | Yes      | Boolean         | false           | When `true`, each assignee receives a separate todo and inspection.         |
| entity_item_specific_assignments     | Yes      | Boolean         | false           | When `true`, assignments are specific to the selected entity items.         |
| timezone                             | Yes      | String          | "Europe/Berlin" | IANA timezone name. Unknown values return 422. Omitting it also returns 422. |
| form_templates                       | Yes      | Array           | [1018907909]    | Form template IDs. `[]` is valid.                                           |
| assignees                            | No       | Object or null  | See example     | Assignee users, groups, entity items, and `all_entity_items`.               |
| assignees.users                      | No       | Array or null   | [868746486]     | User IDs.                                                                   |
| assignees.groups                     | No       | Array or null   | [868746478]     | Group IDs.                                                                  |
| assignees.entity_items               | No       | Array or null   | [412578903]     | Entity item IDs.                                                            |
| assignees.all_entity_items           | No       | Boolean         | false           | When `true`, the schedule applies to all entity items.                      |
| supervisors                          | No       | Object or null  | See example     | Supervisor users and groups.                                                |
| supervisors.users                    | No       | Array or null   | [87913847]      | User IDs.                                                                   |
| supervisors.groups                   | No       | Array or null   | []              | Group IDs.                                                                  |
| rule                                 | Yes      | Object          | See below       | Editor recurrence object. See [Recurrence Rule](#recurrence-rule).          |
| reminders                            | Yes      | Array           | See example     | Reminder objects. `[]` is valid. Do not include `id`.                       |

Each reminder object contains:

| Parameter  | Required | Type   | Example     | Description                                      |
|------------|----------|--------|-------------|--------------------------------------------------|
| type       | Yes      | String | "available" | Reminder type, such as `available` or `due`.     |
| direction  | Yes      | String | "before"    | `before` or `after`.                             |
| scale      | Yes      | String | "hour"      | `month`, `week`, `day`, `hour`, or `minute`.     |
| value      | Yes      | Number | 2           | Amount in the given scale.                       |

The server derives the reminder minute offset from `direction`, `scale`, and `value`. Do not send `time_shift` on create or update.

> An unknown timezone returns:

```json
{
  "message": "The given data was invalid.",
  "errors": {
    "timezone": [
      "The selected timezone is invalid."
    ]
  }
}
```

Omitting required `timezone` also returns 422 with an error on `timezone`.

> An inaccessible related ID returns:

```json
{
  "message": "The given data was invalid.",
  "errors": {
    "form_templates": [
      "The selected form templates is invalid."
    ]
  }
}
```

## Recurrence Rule

Create and update require a `rule` object. Retrieve returns the stored `rrule` string instead of this object.

Supported non-custom `repeat` values are `daily`, `weekday`, `weekly`, `monthly`, `yearly`, and `no-repeat`. Custom rules use `repeat` of `custom` with `frequency` of `weekly` or `monthly`.

`start` is a Unix timestamp. `interval` is required.

> Daily:

```json
{
  "start": 1730117785,
  "repeat": "daily",
  "interval": 1
}
```

> Weekday:

```json
{
  "start": 1730117785,
  "repeat": "weekday",
  "interval": 1
}
```

> Does not repeat:

```json
{
  "start": 1730117785,
  "repeat": "no-repeat",
  "interval": 1
}
```

> Custom weekly. `weekly` is a list of `MO`, `TU`, `WE`, `TH`, `FR`, `SA`, `SU`:

```json
{
  "start": 1730117785,
  "repeat": "custom",
  "interval": 1,
  "frequency": "weekly",
  "weekly": ["MO", "WE"]
}
```

> Custom monthly. `monthly.day` is a weekday code, `day`, `weekday`, or `weekend-day`. `monthly.setpos` is the occurrence in the month:

```json
{
  "start": 1730117785,
  "repeat": "custom",
  "interval": 1,
  "frequency": "monthly",
  "monthly": {
    "day": "MO",
    "setpos": 2
  }
}
```

> Custom monthly on a weekend day:

```json
{
  "start": 1730117785,
  "repeat": "custom",
  "interval": 1,
  "frequency": "monthly",
  "monthly": {
    "day": "weekend-day",
    "setpos": -1
  }
}
```

These are the editor shapes Lumiform already accepts. The API is not a comprehensive RFC RRULE validator.

## Update a Schedule

```shell
curl --request PUT \
  --url 'https://public-api.lumiformapp.com/api/v2/schedules/739184205' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Temple opening","due_in":90,"expire_after_days":7,"separate_todo_for_all_users":false,"entity_item_specific_assignments":false,"timezone":"Europe/Berlin","form_templates":[1018907909],"assignees":{"users":[868746486],"groups":[868746478],"entity_items":[412578903],"all_entity_items":false},"supervisors":{"users":[87913847],"groups":[]},"rule":{"start":1730117785,"repeat":"custom","interval":1,"frequency":"weekly","weekly":["MO","WE"]},"reminders":[{"id":576577251,"type":"available","direction":"before","scale":"hour","value":2}]}'
```

> Request body. Include every field you want to keep, including `form_templates`, `reminders`, and `timezone`:

```json
{
  "title": "Temple opening",
  "due_in": 90,
  "expire_after_days": 7,
  "separate_todo_for_all_users": false,
  "entity_item_specific_assignments": false,
  "timezone": "Europe/Berlin",
  "form_templates": [1018907909],
  "assignees": {
    "users": [868746486],
    "groups": [868746478],
    "entity_items": [412578903],
    "all_entity_items": false
  },
  "supervisors": {
    "users": [87913847],
    "groups": []
  },
  "rule": {
    "start": 1730117785,
    "repeat": "custom",
    "interval": 1,
    "frequency": "weekly",
    "weekly": ["MO", "WE"]
  },
  "reminders": [
    {
      "id": 576577251,
      "type": "available",
      "direction": "before",
      "scale": "hour",
      "value": 2
    }
  ]
}
```

> The above command does not return any data

This endpoint fully replaces a schedule. PATCH is not supported. Use PUT and send the complete writable representation. The request body matches [Create a Schedule](#create-a-schedule), with one difference for reminders: `id` is optional. An existing reminder ID updates that reminder and must belong to the schedule being updated. Omitting `id` creates a reminder. Reminders left out of the array are removed.

`form_templates: []` and `reminders: []` clear those collections. `timezone` is required. Do not send `rrule` or `status`.

A schedule from another organization returns 403. An unknown or deleted schedule returns 404.

### HTTP Request

`PUT https://public-api.lumiformapp.com/api/v2/schedules/<ScheduleId>`

### URL Parameters

| Parameter  | Required | Type   | Example   | Description                      |
|------------|----------|--------|-----------|----------------------------------|
| ScheduleId | Yes      | Number | 739184205 | The ID of the schedule to update. |

> Clearing templates and reminders:

```json
{
  "title": "Temple opening",
  "due_in": 90,
  "expire_after_days": 7,
  "separate_todo_for_all_users": false,
  "entity_item_specific_assignments": false,
  "timezone": "Europe/Berlin",
  "form_templates": [],
  "assignees": {
    "users": [868746486],
    "groups": [868746478],
    "entity_items": [412578903],
    "all_entity_items": false
  },
  "supervisors": {
    "users": [87913847],
    "groups": []
  },
  "rule": {
    "start": 1730117785,
    "repeat": "daily",
    "interval": 1
  },
  "reminders": []
}
```

## Delete a Schedule

```shell
curl --request DELETE \
  --url 'https://public-api.lumiformapp.com/api/v2/schedules/739184205' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> The above command does not return any data

This endpoint deletes a specific schedule.

A schedule from another organization returns 403. An unknown or deleted schedule returns 404.

### HTTP Request

`DELETE https://public-api.lumiformapp.com/api/v2/schedules/<ScheduleId>`

### URL Parameters

| Parameter  | Required | Type   | Example   | Description                      |
|------------|----------|--------|-----------|----------------------------------|
| ScheduleId | Yes      | Number | 739184205 | The ID of the schedule to delete. |

## Decode an RRULE

```shell
curl --request POST \
  --url 'https://public-api.lumiformapp.com/api/v2/rrules/decode' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"rrule":"DTSTART:20241028T121625Z\nRRULE:FREQ=DAILY;BYDAY=MO,WE"}'
```

> Request body:

```json
{
  "rrule": "DTSTART:20241028T121625Z\nRRULE:FREQ=DAILY;BYDAY=MO,WE"
}
```

> The above command returns JSON structured like this:

```json
{
  "rule": {
    "start": 1730117785,
    "repeat": "custom",
    "interval": 1,
    "frequency": "weekly",
    "weekly": ["MO", "WE"]
  }
}
```

This endpoint turns a stored `rrule` string into the editor `rule` object used by create and update. Custom weekly rules return `weekly` as a list of weekday codes, ready to send back on update.

Use this flow to edit a schedule:

1. [Get](#get-a-specific-schedule) the schedule and read its stored `rrule`.
2. POST that string to `/api/v2/rrules/decode`.
3. Edit the returned `rule`.
4. Map related resource objects from retrieve to their IDs.
5. [Update](#update-a-schedule) the schedule with the complete representation, including the edited `rule`.

The endpoint supports editor-representable forms handled by Lumiform's existing decoder. It is not a comprehensive RFC validator or canonicalizer.

Malformed RRULE syntax and frequencies rejected by the existing decoder return a 422 validation error on `rrule` using `validation.rrule.invalid`.

### HTTP Request

`POST https://public-api.lumiformapp.com/api/v2/rrules/decode`

### Request Body Parameters

| Parameter | Required | Type   | Example | Description                        |
|-----------|----------|--------|---------|------------------------------------|
| rrule     | Yes      | String | See above | The stored recurrence string.    |

> A malformed RRULE or a frequency the decoder rejects returns:

```json
{
  "code": "api.validation.errors",
  "message": "The given data was invalid.",
  "errors": {
    "rrule": [
      "validation.rrule.invalid"
    ]
  }
}
```
