---
hidden: true
---

# Handling Errors

Our Client libraries raise exceptions for many reasons, such as a failed charge, invalid parameters, authentication errors, and network unavailability. We recommend writing code that gracefully handles all possible API exceptions.

***

{% columns %}
{% column width="41" %}
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
{% column width="41" %}
**`property_error`**

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
{% column width="41" %}
**`idempotency_error`**

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
{% column width="41" %}
**`invalid_request_error`**

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
