# Approvals

## Get a Specific Approval

```shell
curl --request GET \
  --url 'https://public-api.lumiformapp.com/api/v2/approvals/1' \
  --header 'Authorization: Bearer [your token here]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json'
```

> For an approval on a form, the above command returns JSON structured like this:

```json
{
  "data": {
    "id": 30,
    "status": "approved",
    "comment": "my comment",
    "approver": {
      "id": 4,
      "name": "Jeff Hanneman",
      "email": "jeff.hanneman@slayer.net",
      "admin": 1
    },
    "updated_at": 1748878859,
    "form_id": 12,
    "action_id": null
  }
}
```

> For an approval on an action, it returns JSON structured like this:

```json
{
  "data": {
    "id": 31,
    "status": "pending",
    "comment": null,
    "approver": null,
    "updated_at": 1748878900,
    "form_id": null,
    "action_id": 57
  }
}
```

This endpoint retrieves a specific approval. It uses the standard Bearer token, like every other endpoint.

The `model_id` of the `inspection_approved` webhook is the approval ID. Use this endpoint to find the form behind a webhook. This endpoint, not `approval.id` on a form, is the source of truth for the approval behind a webhook ID.

The response describes the approval's current state (`status`, `comment`, `approver` and `updated_at`), not its state when the webhook was sent. The state can change after the webhook, including back to `pending` (with `comment` cleared) when the form is edited or the approval is reset in the web app. The same approval ID can be delivered more than once, so always read the current status from this endpoint.

A form can have more than one approval over its lifetime. Each webhook carries the ID of the approval that was approved, and this endpoint reports that approval's own status.

### HTTP Request

`GET https://public-api.lumiformapp.com/api/v2/approvals/<ApprovalId>`

### URL Parameters

| Parameter  | Required | Type   | Example | Description                         |
|------------|----------|--------|---------|-------------------------------------|
| ApprovalId | Yes      | Number | 1       | The ID of the approval to retrieve. |

<aside class="notice">
An approval from another organization returns <code>403</code>. An unknown or deleted approval returns <code>404</code>. For an ID from a webhook, a <code>404</code> is final: the approval was deleted, for example together with its form.
</aside>

### Response Fields

| Field      | Type           | Description                                                                                                                                                                         |
|------------|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | Number         | The ID of the approval.                                                                                                                                                             |
| status     | Text           | The current status of the approval. **Allowed values:** *pending*, *approved*, *rejected*, *changes_requested*.                                                                     |
| comment    | Text or null   | The approval comment.                                                                                                                                                               |
| approver   | Object or null | The user who last acted on the approval: changed or reset its status, or edited the form. `null` when no user did, or when that user was deleted.                                  |
| updated_at | Unix time      | When the approval was last updated.                                                                                                                                                 |
| form_id    | Number or null | The ID of the form the approval belongs to. Use it directly on [Get a Specific Form](#get-a-specific-form) (`GET /v2/forms/{id}`). `null` for approvals on actions.               |
| action_id  | Number or null | The ID of the action the approval belongs to. Use it directly on [Get a Specific Action](#get-a-specific-action) (`GET /v2/actions/{id}`). `null` for approvals on forms.         |

Both `form_id` and `action_id` are always present, and exactly one of them is not `null`. For approvals on actions, `action_id` is set and `form_id` is `null`.
