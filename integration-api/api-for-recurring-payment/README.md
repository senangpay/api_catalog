---
icon: arrows-repeat
---

# API for Recurring Payment

If you have your own system and wish to integrate it to senangPay for recurring payments you will need to first add your product into senangPay. The product needs to be created first for auditing purposes. Recurring payments is not available for merchants who subscribe with senangPay x Stripe Package.



To start, we will need the information as below. These can be retrieved from the senangPay Dashboard.

1\. Go to **Menu > Settings > Profile**&#x20;

2\. Refer to the Shopping Cart Integration Link section. Get your **Merchant ID** and **Secret Key** information.

3\. Then  you will need to fill in the **Recurring Return URL**. This is the URL where senangPay will redirect the buyer to after the payment has been processed.

4\. Next, you need to fill in the Recurring Callback URL. Recurring Callback URL is used as an alternative notification to the merchant shopping cart in case here is a breakdown in the transaction flow. For more info on Callback URL, read [here](https://guide.senangpay.my/callback-url/).



## **Getting the Recurring ID**

The Recurring ID is a unique identifier for your recurring product. To obtain it, you'll need to first create a recurring product in the senangPay dashboard.

Here’s a step-by-step guide:

1\. **Create a New Product**

* Navigate to **Menu > Product > Create New** in your senangPay dashboard.

2\. **Set Up the Recurring Product**:

* Choose to create either an **Instalment Product** or a **Subscription Product**. For detailed instructions on setting up these products, refer to the following guides:
  * [Instalment Product Creation](https://guide.senangpay.my/recurring-payment-instalment/)
  * [Subscription Product Creation](https://guide.senangpay.my/recurring-payment-subscription/)

3\. **Find the Recurring ID**:

* After creating the recurring product, go to the product details page.
* Scroll down to the **Payment Frequency Setting** section.
* Locate the Recurring ID under the **Recurring Type** heading.





## **Parameters to send to senangPay**

Below are the details of the elements in the table:

<table><thead><tr><th width="148">Item</th><th>Detail</th></tr></thead><tbody><tr><td><code>order_id</code></td><td><p>Identifies the shopping cart when redirecting after payment. Max 100 characters. </p><ul><li>Allowed: A-Z, a-z, 0-9, and dash ( - )</li><li>Example: 3432D4.</li></ul></td></tr><tr><td><code>recurring_id</code></td><td>Identifies which recurring product/item senangPay processes.</td></tr><tr><td><code>hash</code></td><td>Ensures data integrity between the merchant’s cart and senangPay. Refer to the ‘<a href="generate-secure-hash-recurring-payment.md#how-to-generate-the-secure-hash">How to generate the secure hash</a>’ section for details.</td></tr><tr><td><code>name</code></td><td>Adds the customer's name automatically. It's optional and can be edited.</td></tr><tr><td><code>email</code></td><td>Populates the customer's email for them. Optional and can be modified.</td></tr><tr><td><code>phone</code></td><td>Inserts the customer's phone number. Optional and adjustable by the customer.</td></tr></tbody></table>





{% swagger src="../../.gitbook/assets/swagger phase 1_update code.yaml" path="/recurring/payment/{merchantID}" method="post" %}
[swagger phase 1_update code.yaml](<../../.gitbook/assets/swagger phase 1_update code.yaml>)
{% endswagger %}



## Handles 'Return' & 'Callback' from senangPay

1\. The parameters will be sent using **GET** method.

2\. The parameters are sent to URL as configured in the **Recurring Return URL**. Refer to **‘Information Required’** section

Below are the details of the elements in the table:

| Item             | Detail                                                                                                                                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `status_id`      | <p>Indicates payment status</p><ul><li>1 for success</li><li>0 for failure</li><li>3 for pending (first recurring payment only)</li></ul>                                                                          |
| `order_id`       | Identifies the order sent to senangPay, linking the transaction to your application.                                                                                                                               |
| `msg`            | <p>Describes the payment status. Max 100 characters. Replace underscores with spaces when displaying to customers. </p><ul><li>Example: "Payment_was_successful."</li></ul>                                        |
| `transaction_id` | <p>senangPay's unique transaction ID. Max 100 characters. </p><ul><li>Example: 14363538840. </li></ul><p>Use it to track transactions in senangPay.</p>                                                            |
| `hash`           | Ensures data integrity from senangPay to your shopping cart. See the ‘[How to verify the secure hash](generate-secure-hash-recurring-payment.md#how-to-verify-if-the-secure-hash-is-correct)’ section for details. |





\
\
