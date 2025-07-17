# Handling Errors

Our Client libraries raise exceptions for many reasons, such as a failed charge, invalid parameters, authentication errors, and network unavailability. We recommend writing code that gracefully handles all possible API exceptions.

{% tabs %}
{% tab title="Javascript" %}
```javascript
// Callback style
propAI.properties.search({location: 'Dubai Marina'}, function(err, result) {
  if (err) {
    // Handle error
  } else {
    // Handle success
  }
});

// Promise style
propAI.properties.search({location: 'Dubai Marina'}).then(
  function(result) {
    // Handle success
  },
  function(err) {
    // Handle error
  }
);

switch (err.type) {
  case 'PropAIPropertyError':
    // Property data unavailable or invalid
    err.message; // => e.g. "Property data not available for this Dubai location."
    break;
  case 'PropAIRateLimitError':
    // Too many requests made to the API too quickly
    break;
  case 'PropAIInvalidRequestError':
    // Invalid parameters were supplied to Prop-AI's API
    break;
  case 'PropAIAPIError':
    // An error occurred internally with Prop-AI's API
    break;
  case 'PropAIConnectionError':
    // Some kind of error occurred during the HTTPS communication
    break;
  case 'PropAIAuthenticationError':
    // You probably used an incorrect API key
    break;
  default:
    // Handle any other types of unexpected errors
    break;
}
```
{% endtab %}

{% tab title="Python" %}
```python
import propai

try:
    # Use Prop-AI's library to make requests...
    result = propai.Property.search(location='Dubai Marina')
    pass
except propai.error.PropertyError as e:
    # Property data unavailable, invalid location, or market analysis failed
    print('Status is: %s' % e.http_status)
    print('Code is: %s' % e.code)
    print('Param is: %s' % e.param)  # e.g. 'location' or 'property_type'
    print('Message is: %s' % e.user_message)
except propai.error.RateLimitError as e:
    # Too many requests made to the API too quickly
    pass
except propai.error.InvalidRequestError as e:
    # Invalid parameters were supplied to Prop-AI's API
    # e.g. invalid Dubai coordinates, unsupported emirate
    pass
except propai.error.AuthenticationError as e:
    # Authentication with Prop-AI's API failed
    # (maybe you changed API keys recently)
    pass
except propai.error.APIConnectionError as e:
    # Network communication with Prop-AI failed
    pass
except propai.error.PropAIError as e:
    # Display a very generic error to the user, and maybe send
    # yourself an email
    pass
except Exception as e:
    # Something else happened, completely unrelated to Prop-AI
    pass
```
{% endtab %}
{% endtabs %}

***

### Error Types

{% columns %}
{% column width="41.66666666666667%" %}
#### `api_error`

API errors cover any other type of problem (e.g., a temporary problem with Prop-AI's servers or property data providers), and are extremely uncommon.
{% endcolumn %}

{% column %}
<pre class="language-json"><code class="lang-json">{
  "error": {
    "type": "api_error",
<strong>    "message": "Unable to connect to property          data service"
</strong>  }
}
</code></pre>
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column width="41.66666666666667%" %}
#### `property_error`

Property errors are the most common type of error you should expect to handle. They result when the requested property data is unavailable, invalid, or when market analysis cannot be performed.
{% endcolumn %}

{% column %}
```json
{
  "error": {
    "type": "property_error",
    "code": "property_not_found",
    "message": "Property data not available for this Dubai location"
  }
}
```
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column width="41.66666666666667%" %}
#### `idempotency_error`

Idempotency errors occur when an Idempotency-Key is re-used on a request that does not match the first request's API endpoint and parameters.
{% endcolumn %}

{% column %}
```json
{
  "error": {
    "type": "idempotency_error",
    "message": "Idempotency key used with different parameters"
  }
}
```
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column width="41.66666666666667%" %}
#### `invalid_request_error`

Invalid request errors arise when your request has invalid parameters (e.g., invalid property coordinates, unsupported location in Middle East, missing required fields).
{% endcolumn %}

{% column %}
```json
{
  "error": {
    "type": "invalid_request_error",
    "param": "location",
    "message": "Location must be within Dubai or supported Middle East markets"
  }
}
```
{% endcolumn %}
{% endcolumns %}
