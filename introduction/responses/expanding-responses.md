# Expanding Responses

Many objects allow you to request additional information as an expanded response by using the `expand` request parameter. This parameter is available on all API requests, and applies to the response of that request only. You can expand responses in two ways.

{% columns fullWidth="false" %}
{% column width="41" %}
#### Expanding Related Objects

In many cases, an object contains the ID of a related object in its response properties. For example, a `Property` might have an associated Developer ID or Market Analysis ID. You can expand these objects in line with the expand request parameter. The `expandable` label in this documentation indicates ID fields that you can expand into objects.
{% endcolumn %}

{% column %}
```javascript
// Expand a property's developer information
propAI.properties.retrieve('prop_1234', {
  expand: ['developer']
});
```
{% endcolumn %}
{% endcolumns %}

{% columns fullWidth="false" %}
{% column width="41" %}
#### Expanding Hidden Fields

Some available fields aren't included in the responses by default, such as the `owner_contact` and `internal_notes` fields for the Property object. You can request these fields as an expanded response by using the `expand` request parameter.
{% endcolumn %}

{% column %}
```javascript
// Expand multiple related objects
propAI.properties.retrieve('prop_1234', {
  expand: ['developer', 'market_analysis', 'location_data']
});
```
{% endcolumn %}
{% endcolumns %}

{% columns fullWidth="false" %}
{% column width="41" %}
#### Recursive Expansion

You can expand recursively by specifying nested fields after a dot (`.`). For example, requesting `market_analysis.developer` on a property expands the `market_analysis` property into a full Market Analysis object, then expands the `developer` property on that market analysis into a full Developer object.
{% endcolumn %}

{% column %}
```javascript
// Recursive expansion
propAI.properties.retrieve('prop_1234', {
  expand: ['market_analysis.developer.projects']
});
```
{% endcolumn %}
{% endcolumns %}

***

{% hint style="success" %}
Expansions have a maximum depth of four levels (for example, the deepest expansion allowed when listing properties is `data.market_analysis.developer.parent_company`).
{% endhint %}

### Endpoint Compatibility

You can use the `expand` parameter on any endpoint that returns expandable fields, including list, create, and update endpoints.

{% columns fullWidth="false" %}
{% column width="41" %}
#### List Request Expansions

Expansions on list requests start with the `data` property. For example, you can expand `data.developer` on a request to list properties and associated developers. Performing deep expansions on numerous list requests might result in slower processing times.
{% endcolumn %}

{% column %}
```javascript
// Expand developers for all properties in a list
propAI.properties.list({
  location: 'Dubai Marina',
  expand: ['data.developer']
});

// Expand multiple fields for property listings
propAI.properties.list({
  location: 'Business Bay',
  expand: ['data.developer', 'data.market_analysis']
});
```
{% endcolumn %}
{% endcolumns %}

{% columns fullWidth="false" %}
{% column width="41" %}
#### Multiple Object Expansion

You can expand multiple objects at the same time by identifying multiple items in the `expand` array.
{% endcolumn %}

{% column %}
```javascript
propAI.properties.retrieve('prop_1234', {
  expand: [
    'developer',
    'market_analysis',
    'location_data',
    'similar_properties'
  ]
});
```
{% endcolumn %}
{% endcolumns %}
