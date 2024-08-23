---
description: testing page from gitbook edit
---

# Manual Integration API (Open API)

If you have develop your own shopping cart and need manual integration by yourself, here are the details.

**1. Info required(test)**

To start we will need the information as below. These can be retrieve in senangPay Dashboard.

1.1 Go to Menu > Settings > Profile

1.2 Refer to **Shopping Cart Integration Link** section. Get your **Merchant ID** and **Secret Key** information.

1.3 Then you will need to fill in the return URL. This is the URL where senangPay will redirect the buyer after the payment has been processed.

1.4 Next, you need to fill the Callback URL. Callback URL is used as alternative notification to merchant shopping cart in case there is a breakdown in transaction flow. For more info on Callback URL, read [here](https://guide.senangpay.my/callback-url/)

**2. What parameters to send to senangPay**

Below are the details of the elements in the table :

| Item      | Detail                                                                                                                                                                                                                                                                  |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| detail    | This is the description to be displayed when making the payment. The maximum length is 500 characters. Any underscore (\_) characters will be converted to space. Example Shopping\_cart\_id\_30. Only A to Z, a to z, 1 to 0, dot, comma, dash and underscore allowed. |
| amount    | The amount to charge the buyer. The format must be in 2 decimal places. Example 25.50.                                                                                                                                                                                  |
| order\_id | This is the id to be use to identify the shopping cart when senangPay redirect back the buyer after the payment was made. The maximum length is 100 characters. Example 3432D4. Only A to Z, a to z, 1 to 0 and dash allowed.                                           |
| hash      | The is the data to ensure the data integrity passed from merchant’s shopping cart to senangPay. Refer to How to generate the secure hash section for more info.                                                                                                         |
| name      | This is the name to populate in the payment form so that customer do not have to key in their name. This is optional and not have to be part of the hash. Customer is able to overwrite the value in payment form.                                                      |
| email     | This is the email to populate in the payment form so that customer do not have to key in their email. This is optional and not have to be part of the hash. Customer is able to overwrite the value in payment form.                                                    |
| phone     | This is the phone to populate in the payment form so that customer do not have to key in their phone. This is optional and not have to be part of the hash. Customer is able to overwrite the value in payment form.                                                    |



{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/{merchantID}" method="post" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/return" method="get" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger phase 1.yaml" path="/payment/callback" method="post" %}
[swagger phase 1.yaml](<../.gitbook/assets/swagger phase 1.yaml>)
{% endswagger %}
