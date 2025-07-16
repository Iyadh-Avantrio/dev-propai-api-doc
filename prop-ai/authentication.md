---
description: >-
  The Prop-AI API uses API keys to authenticate requests. You can view and
  manage your API keys in the Prop-AI Dashboard (coming soon)
---

# Authentication

### Overview

Test mode secret keys have the prefix `sk_test_` and live mode secret keys have the prefix `sk_live_` Alternatively, you can use _restricted API keys_ for granular permissions.

Use your API key by setting it in the initial configuration of prop-ai. The Node.js library will then automatically send this key in each request.

{% hint style="danger" %}
Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.
{% endhint %}

***

_You can also set a per-request key with an option. This is often useful for Connect applications that use multiple API keys during the lifetime of a process. Methods on the returned object reuse the same API key._

{% hint style="info" %}
All API requests must be made over [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure). Calls made over plain HTTP will fail. API requests without authentication will also fail.
{% endhint %}

### Global API Key

```javascript
const PropAI = require('prop-ai');
const propai = PropAI('sk_test_51Re0ozE6HuHzGiZvRSpuu1inMpkYKIKApaIb973kRwXVGJrLcPO4bSW0FciIVNlx2zVA7SzR3U8WrAtP032gpRgP001acmtRJD');
```

### Per-Request Key

```javascript
var charge = await propai.charges.retrieve( 
    'ch_3LiiC52eZvKYlo2C1da66ZSQ',
    {
        apiKey: 'sk_test_51Re0ozE6HuHzGiZvRSpuu1inMpkYKIKApaIb973kRwXVGJrLcPO4bSW0FciIVNlx2zVA7SzR3U8WrAtP032gpRgP001acmtRJD'
    }
);
```

\
\
