# Connected Accounts

To act as connected accounts, clients can issue requests using the `PropAI`Account special header. Make sure that this header contains a PropAI account ID, which usually starts with the `acct_` prefix.

The value is set per-request as shown in the adjacent code sample. Methods on the returned object reuse the same account ID.

{% hint style="warning" %}
Related guide: [Making API calls for connected accounts](https://docs.stripe.com/connect/authentication)
{% endhint %}

{% tabs %}
{% tab title="JavaScript" %}
```javascript
propai.charges.retrieve('ch_3LmjSR2eZvKYlo2C1cPZxlbL', {
  propaiAccount: 'acct_1032D82eZvKYlo2C'
});
```
{% endtab %}

{% tab title="Python" %}
```python
import propai
charge = propai.Charge.retrieve(
  "ch_3Lmjoz2eZvKYlo2C1rBER4Dk",
  propai_account="acct_1032D82eZvKYlo2C"
)
charge.capture() # Uses the same account.
```
{% endtab %}

{% tab title="PHP" %}
```php
$ch = $propai->charges->retrieve(
  'ch_3Lmjrl2eZvKYlo2C1bscjw8Z',
  [],
  ['propai_account' => 'acct_1032D82eZvKYlo2C']
);
$ch->capture(); // Uses the same account.
```
{% endtab %}
{% endtabs %}
