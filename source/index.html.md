---
title: Lumiform Public API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - filters
  - inspections 
  - issues
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Lumiform Public API documentation! You can use our API to get your organization's Inspections, Issues and much more.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Accept: application/json" \
  -H "Authorization: Bearer yourtoken"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('yourtoken');
```

> Make sure to replace `yourtoken` with your API key.

Lumiform uses API keys to allow access to the API. You can register for a new Lumiform Public API key at our [developer portal](http://example.com/developers).

Lumiform expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer [your token here]`

<aside class="notice">
You must replace <code>[your token here]</code> with your organization's API key.
</aside>
