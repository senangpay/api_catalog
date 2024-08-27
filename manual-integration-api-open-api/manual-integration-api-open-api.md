---
icon: money-check
---

# Manual Integration API (Open API)

If you have develop your own shopping cart and need manual integration by yourself, here are the details.

## **Info required**&#x20;

To start we will need the information as below. These can be retrieve in senangPay Dashboard.

1. Go to Menu > Settings > Profile
2. Refer to **Shopping Cart Integration Link** section. Get your **Merchant ID** and **Secret Key** information.
3. Then you will need to fill in the return URL. This is the URL where senangPay will redirect the buyer after the payment has been processed.
4. &#x20;need to fill the Callback URL. Callback URL is used as alternative notification to merchant shopping cart in case there is a breakdown in transaction flow. For more info on Callback URL, read [here](https://guide.senangpay.my/callback-url/)



## **What parameters to send to senangPay**

Below are the details of the elements in the table :

<table><thead><tr><th width="247">Item</th><th>Detail</th></tr></thead><tbody><tr><td>detail</td><td><p>Description displayed during payment (max 500 characters). Underscores (_) convert to spaces. </p><ul><li>Example: <code>Shopping_cart_id_30</code></li><li>Allowed characters: A-Z, a-z, 0-9, dot ( . ), comma ( , ), dash ( - ), underscore ( _ ).</li></ul></td></tr><tr><td>amount</td><td><p>TThe charge amount, formatted to 2 decimal places.</p><ul><li>Example: <code>25.50</code>.</li></ul></td></tr><tr><td>order_id</td><td><p>Identifies the shopping cart on return after payment (max 100 characters).</p><ul><li>Example: <code>3432D4</code></li><li>Allowed characters: A-Z, a-z, 0-9, dash ( - ).</li></ul></td></tr><tr><td>hash</td><td>Ensures data integrity between the merchant’s cart and senangPay. Refer to the "How to generate the secure hash" section.</td></tr><tr><td>name</td><td>Adds the customer's name automatically. It's optional and can be edited.</td></tr><tr><td>email</td><td>Populates the customer's email for them. Optional and can be modified.</td></tr><tr><td>phone</td><td>Inserts the customer's phone number. Optional and adjustable by the customer.</td></tr></tbody></table>



{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/{merchantID}" method="post" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/return" method="get" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/callback" method="post" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}
