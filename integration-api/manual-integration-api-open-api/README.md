---
icon: money-check
---

# Manual Integration API (Open API)

If you've created your own e-commerce site and require manual integration, here are the details.

## **Information required**&#x20;

To get started, please gather the following details from your senangPay Dashboard:

Go to **Menu > Settings > Profile**

1\. **Merchant ID and Secret Key** : Find these in the **Shopping Cart Integration Link** section.

2\. **Return URL** : Specify the Return URL where senangPay will redirect buyers after payment processing.

3\. **Callback URL** :

* Provide the Callback URL, which serves as an alternative notification method if there is an issue with the transaction flow.
* For more information on the Callback URL, please [read here ->](https://guide.senangpay.my/callback-url/)

Ensure you have these details ready to facilitate a smooth integration process.



## **What parameters to send to senangPay**

Below are the details of the elements in the table :

<table><thead><tr><th width="247">Item</th><th>Detail</th></tr></thead><tbody><tr><td><code>detail</code></td><td><p>Description displayed during payment (max 500 characters). Underscores (_) convert to spaces. </p><ul><li>Example: <code>Shopping_cart_id_30</code></li><li>Allowed characters: A-Z, a-z, 0-9, dot ( . ), comma ( , ), dash ( - ), underscore ( _ ).</li></ul></td></tr><tr><td><code>amount</code></td><td><p>The charge amount, formatted to 2 decimal places.</p><ul><li>Example: <code>25.50</code>.</li></ul></td></tr><tr><td><code>order_id</code></td><td><p>Identifies the shopping cart on return after payment (max 100 characters).</p><ul><li>Example: <code>3432D4</code></li><li>Allowed characters: A-Z, a-z, 0-9, dash ( - ).</li></ul></td></tr><tr><td><code>hash</code></td><td>Ensures data integrity between the merchant’s cart and senangPay. Refer to the "<a href="generate-secure-hash.md#how-to-generate-the-secure-hash">How to generate the secure hash</a>" section.</td></tr><tr><td><code>name</code></td><td>Adds the customer's name automatically. It's optional and can be edited.</td></tr><tr><td><code>email</code></td><td>Populates the customer's email for them. Optional and can be modified.</td></tr><tr><td><code>phone</code></td><td>Inserts the customer's phone number. Optional and adjustable by the customer.</td></tr><tr><td><code>timeout</code> (optional)</td><td><p>Sets the payment timeout in seconds </p><ul><li>Example :  8 minutes = 480 seconds</li></ul><p> If not completed within this time, the payment will expire and redirect to the return URL. <strong>Minimum is 60 seconds</strong>; below this defaults to 60 seconds. No timeout if omitted.</p></td></tr></tbody></table>



{% swagger src="../../.gitbook/assets/swagger spelling checked.yaml" path="/payment/{merchantID}" method="post" %}
[swagger spelling checked.yaml](<../../.gitbook/assets/swagger spelling checked.yaml>)
{% endswagger %}

<mark style="color:red;">\*\* The "Test it" option is available when using Firefox or Safari to test the API</mark>

### Handles 'Return' & 'Callback' from senangPay

1\. The parameters will be send using **GET** method.

2\. The parameters are sent to URL as configured in the [return URL](./#information-required). Refer to the **‘Information Required’** section.

The table below lists the details of the elements:

| Item            | Detail                                                                                                                                                                                                                                                                  |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status\_id      | This is to indicate the status of the payment. It only has 3 values which is ; 2 for **pending authorization**, 1 for **successful** and 0 for **failed.**                                                                                                              |
| order\_id       | This is the order that is sent to senangPay. This is to identify the shopping cart transaction.                                                                                                                                                                         |
| msg             | This is the message to describe the payment status. The maximum length is 100 characters. Take note that the message may contain underscores. You can replace the underscore as space when displaying the message to your customers. Example: Payment\_was\_successful. |
| transaction\_id | This is the transaction ID used by senangPay. You can use this ID to track the transaction in senangPay. The maximum length is 100 characters. Example 14363538840                                                                                                      |
| hash            | This is the data to ensure that data integrity has passed from senangPay to the merchant’s shopping cart. Refer to section ‘[How to verify if the secure hash is correct](generate-secure-hash.md#how-to-verify-if-the-secure-hash-is-correct)’ for more info.          |

3\. **Callback** : The parameter will be send by **POST** method.

