---
description: >-
  The Prop-AI API uses API keys to authenticate requests. You can view and
  manage your API keys in the Prop-AI Dashboard
---

# Authentication

### Overview

Prop-AI uses **API keys** to authenticate all requests. You must include your API key in every request using the `x-api-key` header.

### Getting Your API Key

1. Visit your [Prop-AI Dashboard](https://prop-ai.com)
2. Go to the **Settings** section.
3. Under **API Keys**, click **Generate New API Key**.
4. **Copy the API key** and store it securely — it will not be shown again.
5. Lost it? No worries — just delete the old one and generate a new key

{% hint style="danger" %}
Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.
{% endhint %}

***

### Example Request

Each request must include your API key in the header as:

```http
x-api-key: YOUR_SECRET_API_KEY
```

{% hint style="info" %}
All API requests must be made over [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure). Calls made over plain HTTP will fail. API requests without authentication will also fail.
{% endhint %}

{% tabs %}
{% tab title="JavaScript" %}
```javascript
const axios = require('axios');

const API_KEY = 'prop-ai_1234567890abcdef';

axios.get('https://api.prop-ai.com/v1/listings', {
  headers: {
    'x-api-key': API_KEY,
    'Content-Type': 'application/json'
  }
})
.then(response => {
  console.log('Data:', response.data);
})
.catch(error => {
  console.error('Error:', error.response?.data || error.message);
});

```
{% endtab %}

{% tab title="Python" %}
```python
import requests

API_KEY = 'prop-ai_1234567890abcdef'
url = 'https://api.prop-ai.com/v1/listings'

headers = {
    'x-api-key': API_KEY,
    'Content-Type': 'application/json'
}

response = requests.get(url, headers=headers)

if response.ok:
    print("Data:", response.json())
else:
    print("Error:", response.status_code, response.text)

```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$apiKey = 'prop-ai_1234567890abcdef';
$url = 'https://api.prop-ai.com/v1/listings';

$ch = curl_init($url);

curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'x-api-key: ' . $apiKey,
    'Content-Type: application/json'
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);

if (curl_errno($ch)) {
    echo 'Curl error: ' . curl_error($ch);
} else {
    $http_code = curl_getinfo($ch, CURLINFO_HTTP_CODE);
    if ($http_code === 200) {
        echo 'Data: ' . $response;
    } else {
        echo "Error: HTTP $http_code\n$response";
    }
}

curl_close($ch);

```
{% endtab %}
{% endtabs %}
