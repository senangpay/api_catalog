---
icon: money-check
---

# Manual Integration API (Open API)

If you've created your own e-commerce site and require manual integration, here are the details.

## **Information required**&#x20;

To get started, please gather the following details from your senangPay Dashboard:

Go to **Menu** > **Settings** > **Profile**

1\. **Merchant ID and Secret Key :** Find these in the **Shopping Cart Integration Link** section.

2\. **Return URL** : Specify the Return URL where senangPay will redirect buyers after payment   processing.

3\. **Callback URL :**&#x20;

* Provide the Callback URL, which serves as an alternative notification method if there is an issue with the transaction flow.
* For more information on the Callback URL, please [read here ->](https://guide.senangpay.my/callback-url/)



&#x20;

Ensure you have these details ready to facilitate a smooth integration process.



## **What parameters to send to senangPay**

Below are the details of the elements in the table :

<table><thead><tr><th width="247">Item</th><th>Detail</th></tr></thead><tbody><tr><td><code>detail</code></td><td><p>Description displayed during payment (max 500 characters). Underscores (_) convert to spaces. </p><ul><li>Example: <code>Shopping_cart_id_30</code></li><li>Allowed characters: A-Z, a-z, 0-9, dot ( . ), comma ( , ), dash ( - ), underscore ( _ ).</li></ul></td></tr><tr><td><code>amount</code></td><td><p>TThe charge amount, formatted to 2 decimal places.</p><ul><li>Example: <code>25.50</code>.</li></ul></td></tr><tr><td><code>order_id</code></td><td><p>Identifies the shopping cart on return after payment (max 100 characters).</p><ul><li>Example: <code>3432D4</code></li><li>Allowed characters: A-Z, a-z, 0-9, dash ( - ).</li></ul></td></tr><tr><td><code>hash</code></td><td>Ensures data integrity between the merchant’s cart and senangPay. Refer to the "How to generate the secure hash" section.</td></tr><tr><td><code>name</code></td><td>Adds the customer's name automatically. It's optional and can be edited.</td></tr><tr><td><code>email</code></td><td>Populates the customer's email for them. Optional and can be modified.</td></tr><tr><td><code>phone</code></td><td>Inserts the customer's phone number. Optional and adjustable by the customer.</td></tr></tbody></table>



{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/{merchantID}" method="post" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/return" method="get" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/callback" method="post" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}
