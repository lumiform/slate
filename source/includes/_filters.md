# Filters
<aside class="success">
Tip — use these endpoints to help you filter resources!
</aside>

## Get All Users

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
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

`GET http://public-api.lumiformdev.com/api/v1/filters/users`

## Get All Sites

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
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

`GET http://public-api.lumiformdev.com/api/v1/filters/sites`
