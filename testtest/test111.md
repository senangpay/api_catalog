---
icon: lock-a
---

# API for Recurring Payment

If you have your own system and wish to integrate it to senangPay for recurring payments you will need to first add your product into senangPay. The product needs to be created first for auditing purposes. Recurring payments is not available for merchants who subscribe with senangPay x Stripe Package.



To start, we will need the information as below. These can be retrieved from the senangPay Dashboard.

1. Go to Menu > Settings > Profile
2. Refer to the Shopping Cart Integration Link section. Get your Merchant ID and Secret Key information.
3. Then you will need to fill in the **Recurring Return URL**. This is the URL where senangPay will redirect the buyer to after the payment has been processed.
4. Next, you need to fill in the Recurring Callback URL. Recurring Callback URL is used as an alternative notification to the merchant shopping cart in case here is a breakdown in the transaction flow. For more info on Callback URL, read [here](https://guide.senangpay.my/callback-url/).



## **Getting the Recurring ID**

Recurring id is the unique id that identifies your recurring product. To obtain the recurring id, you must first create a recurring product in senangPay dashboard.

1\. Go to Menu >Product > Create New

2\. Creating a recurring product. You can learn more on how to create a recurring product here at these links.

* &#x20;[Instalment Product](https://guide.senangpay.my/recurring-payment-instalment/)
* &#x20;[Subscription Product](https://guide.senangpay.my/recurring-payment-subscription/)

3\. Once the recurring product has been created, view the product details page, scroll down to **Payment Frequency Setting** section. The **Recurring Id** is located under Recurring Type.



## **Parameters to send to senangPay**

Below are the details of the elements in the table:

<table><thead><tr><th width="181">Item</th><th>Detail</th></tr></thead><tbody><tr><td><code>order_id</code></td><td><p>This is the id used to identify the shopping cart when senangPay redirects the buyer back after the payment was made. The maximum length is 100 characters. </p><p>Example :  3432D4. <strong>Only A to Z, a to z, 1 to 0 and dash allowed</strong>.</p></td></tr><tr><td><code>recurring_id</code></td><td>This is the id used to identify which recurring product/item senangPay needs to process.</td></tr><tr><td><code>hash</code></td><td>This is the data to ensure that data integrity has passed from the merchant’s shopping cart to senangPay. Refer to ‘How to generate the secure hash’ section for more info.</td></tr><tr><td><code>name</code></td><td>This is the name to populate in the payment form so that customers do not have to key in their names. This is optional and does not have to be a part of the hash. Customers are able to overwrite the value in the payment form.</td></tr><tr><td><code>email</code></td><td>This is the email to populate in the payment form so that customers do not have to key in their emails. This is optional and does not have to be a part of the hash. Customers are able to overwrite the value in the payment form.</td></tr><tr><td><code>phone</code></td><td>This is the phone number to populate in the payment form so that customers do not have to key in their phone. This is optional and does not have to be a part of the hash. Customers are able to overwrite the value in payment form.</td></tr></tbody></table>





{% swagger src="../.gitbook/assets/manual-api.yaml" path="/payment" method="get" %}
[manual-api.yaml](../.gitbook/assets/manual-api.yaml)
{% endswagger %}

## **What Parameters does the shopping cart receive from senangPay**

Below are the details of the elements in the table:

| Item             | Detail                                                                                                                                                                                                                                                                |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `status_id`      | This is to indicate the status of the payment. The values will be received are 1 for successful, 0 for failed and 3 for Pending Payment for Recurring Schedule (First time only).                                                                                     |
| `order_id`       | This is the order that was sent to senangPay. This is to identify the transaction generated from your application.                                                                                                                                                    |
| `msg`            | This is the message to describe the payment status. The maximum length is 100 characters. Take note that the message may contain underscores. You can replace the underscore as space when displaying the message to your customer. Example Payment\_was\_successful. |
| `transaction_id` | This is the transaction ID used by senangPay. You can use this ID to track the transaction in senangPay. The maximum length is 100 characters. Example 14363538840                                                                                                    |
| `hash`           | This is the data to ensure that data integrity has passed from senangPay to the merchant’s shopping cart. Refer to the section ‘How to verify if the secure hash’ is correct for more information.                                                                    |

## **How senangPay sends the parameters to merchant’s shopping cart**

1\. The parameters will be sent using GET method.

2\. The parameters are sent to URL as configured in the Recurring Return URL. Refer to ‘Info Required’ section



## **How to generate the secure hash**

1\. The secure hash is generated by using sha256 on a string consisting of (according to sequence):

* Secret Key
* Recurring ID
* Order ID

2\. For example if the values for the parameters are as in PHP  shown below :&#x20;



```php

?php
/$secret_key = ‘21245-957’;
$recurring_id = ‘1234’;
$order_id = ’12’;

$hash = hash(‘sha256’,$secret_key.$recurring_id.$order_id);

?>

```

3\. So, the string to be hashed is **21245-957123412,** which will generate the hash values of:

* **a8167dd09f01ebed0b18e67b2cc2424a0d058ccc83d94803482ecdeedff7728f**



## **How to verify if the secure hash is correct**

1\. Merchansts will need to generate the secure hash and compare the secure hash that was received from senangPay.

2\. For example, if the parameters received from senangPay are as in PHP shown below :&#x20;



```php

$status_id = '1';
$order_id = '12';
$transaction_id = '14363538840';
$msg = 'Payment_was_successful';

$hash = hash(‘sha256’,$secret_key.$status_id.$order_id.$transaction_id.$msg);

?>

```

3\. So, the string to be hashed is **21245-95711214363538840Payment\_was\_successful,** which will generate the hash values of:

* **24354422953c29bf4b822f6783bbaf64ef445623d6e8ea4ddc1582a29c03cda0**

4\. Compare the hash value that you have generated with the hash value sent from senangPay. If the value does not match then the data may have been tampered with.

\
\
