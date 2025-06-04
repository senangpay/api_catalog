---
icon: arrows-repeat
---

# API for Recurring Payment

If you have your own system and wish to integrate it to senangPay for recurring payments, you will first need to add your products into senangPay. The products need to be created first for auditing purposes. Recurring payments are not available for merchants who subscribe to the senangPay x Stripe package (legacy package).



To start, we will need the information below. These can be retrieved from the senangPay dashboard.

1\. Go to **Menu > Settings > Profile**.

2\. Refer to the "Shopping Cart Integration Link" section. Get your **Merchant ID** and **Secret Key** information.

3\. Then  you will need to fill in the **Recurring Return URL**. This is the URL where senangPay will redirect the buyer to after the payment has been processed.

4\. Next, fill in the Recurring Callback URL. Recurring Callback URL is used as an alternative notification to the merchant shopping cart in case there is a breakdown in the transaction flow. For more info on Callback URL, read [here](https://guide.senangpay.my/callback-url/).



## **Getting the Recurring ID**

The Recurring ID is a unique identifier for your recurring payment product. To obtain it, you'll need to first create a recurring payment product in the senangPay dashboard.

Here’s a step-by-step guide:

1\. **Create a new product**

* Navigate to **Menu > Product > Create New** in your senangPay dashboard.

2\. **Set up the recurring product**:

* Choose to create either an **Instalment Product** or a **Subscription Product**. For detailed instructions on setting up these products, refer to the following guides:
  * [Instalment Product Creation](https://guide.senangpay.my/recurring-payment-instalment/)
  * [Subscription Product Creation](https://guide.senangpay.my/recurring-payment-subscription/)

3\. **Find the Recurring ID**:

* After creating the recurring product, go to the product details page.
* Scroll down to the **Payment Frequency Setting** section.
* Locate the Recurring ID under the **Recurring Type** heading.



## **Parameters to send to senangPay**

Below are the details of the elements in the table:

<table><thead><tr><th width="148">Item</th><th>Detail</th></tr></thead><tbody><tr><td><code>order_id</code></td><td><p>Identifies the shopping cart when redirecting after payment. Maximum length is 100 characters. </p><ul><li>Allowed: A-Z, a-z, 0-9, and dash (-)</li><li>Example: 3432D4.</li></ul></td></tr><tr><td><code>recurring_id</code></td><td>Identifies which recurring product/item senangPay processes.</td></tr><tr><td><code>hash</code></td><td>Ensures data integrity between the merchant’s cart and senangPay. Refer to <a href="../manual-integration-api-open-api/generate-secure-hash.md#how-to-generate-a-secure-hash">the "How to generate a secure hash" section</a> for details.</td></tr><tr><td><code>name</code></td><td>Adds the customer's name automatically. This is optional and can be edited.</td></tr><tr><td><code>email</code></td><td>Populates the customer's e-mail for them. This is optional and can be edited.</td></tr><tr><td><code>phone</code></td><td>Inserts the customer's phone number. This is optional and adjustable by the customer.</td></tr></tbody></table>



{% openapi src="../../.gitbook/assets/swagger- endpoint sandbox api_.yaml" path="/recurring/payment/{merchantID}" method="post" %}
[swagger- endpoint sandbox api_.yaml](<../../.gitbook/assets/swagger- endpoint sandbox api_.yaml>)
{% endopenapi %}

<mark style="color:red;">\*The "Test it" option is available when using Firefox or Safari to test the API.</mark>



## Handling 'Return' and 'Callback' from senangPay

1\. The parameters will be sent using **GET** method.

2\. The parameters are sent to URL as configured in the **Recurring Return URL**. Refer to **‘Information Required’** section

Below are the details of the elements in the table:

| Item             | Detail                                                                                                                                                                                                                               |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `status_id`      | <p>Indicates payment status</p><ul><li>1 for success</li><li>0 for failure</li><li>3 for pending (first recurring payment only)</li></ul>                                                                                            |
| `order_id`       | Identifies the order sent to senangPay, linking the transaction to your application.                                                                                                                                                 |
| `msg`            | <p>Describes the payment status. Maximum length is 100 characters. Replace underscores with spaces when displaying to customers. </p><ul><li>Example: "Payment_was_successful."</li></ul>                                            |
| `transaction_id` | <p>senangPay's unique transaction ID. Max 100 characters. </p><ul><li>Example: 14363538840. </li></ul><p>Use it to track transactions in senangPay.</p>                                                                              |
| `hash`           | Ensures data integrity from senangPay to your shopping cart. Refer to [the "How to verify secure hash" section](../manual-integration-api-open-api/generate-secure-hash.md#how-to-verify-if-the-secure-hash-is-correct) for details. |

3\. **Callback**: The parameter will be sent via **POST** method.

\
\
