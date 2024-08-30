---
icon: gear-complex
---

# Tokenization API List

### **1.0 Pay credit card using token**

| Item                            | Detail                                 |
| ------------------------------- | -------------------------------------- |
| **URL endpoint (POST)**         | https://app.senangpay.my/apiv1/pay\_cc |
| **Sandbox URL endpoint (POST)** | https://app.senangpay.my/apiv1/pay\_cc |



### **1.1 Authorization Header (Basic Auth)**

| Type     | Basic                                                                       |
| -------- | --------------------------------------------------------------------------- |
| Username | <p>&#x3C; your-merchant-id ><br>As listed in the profile settings page.</p> |
| Password | None, leave empty.                                                          |



### **1.2 Request Parameter (All Mandatory)**

<table data-header-hidden><thead><tr><th width="267"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter Name</strong></td><td><strong>Parameter value/description</strong></td></tr><tr><td><a data-footnote-ref href="#user-content-fn-1">name</a></td><td><p>Your customer name. Maximum length is 100.</p><ul><li>Example : Abu Bin Ali</li></ul></td></tr><tr><td>email</td><td><p>Your customer email.</p><ul><li>Example :  ahmad@google.com</li></ul></td></tr><tr><td>detail</td><td><p>Your order detail. Maximum length is 100. </p><ul><li>Example : Order for product id #4</li></ul></td></tr><tr><td>phone</td><td><p>Your customer phone number.</p><ul><li>Example : 0109876543</li></ul></td></tr><tr><td>order_id</td><td><p>Your order id. Can be number or string. Other character is invalid. </p><ul><li>Example : 123</li></ul></td></tr><tr><td>amount</td><td><p>Your order amount in integer format. Convert from decimals as necessary.</p><ul><li>Example : if the amount is RM 2.00, you need to send 200.</li></ul></td></tr><tr><td>token</td><td>Generated token from <a href="3d-get-token.md#integration-method">Get Token API</a></td></tr><tr><td>hash</td><td>A string generated using your secret key (found in your profile settings) with the HMAC SHA256 algorithm. The format is as follows:<br><code>&#x3C;your merchant id>&#x3C;name>&#x3C;email>&#x3C;phone>&#x3C;detail>&#x3C;order_id>&#x3C;amount></code><br>*<em>Note: Do not include the <code>&#x3C; ></code> characters.*</em></td></tr></tbody></table>



### **1.3 Response Parameter**

<table data-header-hidden><thead><tr><th width="247"></th><th></th></tr></thead><tbody><tr><td>Parameter Name</td><td><strong>Parameter value / description</strong></td></tr><tr><td>status</td><td>Your transaction status. 1 if successful. 0 if failed.</td></tr><tr><td>transaction_id</td><td>Your transaction ID number.</td></tr><tr><td>order_id</td><td>Your original order ID.</td></tr><tr><td>amount_paid</td><td><p>Amount transacted from the credit card in integer format.</p><ul><li>Example : If the amount transacted is RM 2.00, it will output 200.</li></ul></td></tr><tr><td>msg</td><td>Transaction status message. You'll receive "<em><strong>Payment was successful</strong></em>" for successful payments, or an error message if the transaction failed.</td></tr><tr><td>hash</td><td>A string generated using your secret key with HMAC SHA256. Format:<br><code>&#x3C;merchant_id>&#x3C;status_id>&#x3C;order_id> &#x3C;transaction_id>&#x3C;amount_paid>&#x3C;msg></code><br><em>Exclude the <code>&#x3C; ></code> characters.</em></td></tr></tbody></table>

### **1.4 Sample Response**

```javascript
{
   "status":1,
   "transaction_id":"14951544812820",
   "order_id":"1234",
   "amount_paid":1000,
   "msg":"Payment was successful",
   "hash":"99b6e99bb0aa663101b1e4f6f8d69c2efb41ef81a5a7aa030bf76a098a03d233"
}

```



{% swagger src="../../.gitbook/assets/swagger phase 1_update code.yaml" path="/apiv1/pay_cc" method="post" %}
[swagger phase 1_update code.yaml](<../../.gitbook/assets/swagger phase 1_update code.yaml>)
{% endswagger %}

###

### **2.0 Enable/disable credit card**

| **Item**                | **Detail**                                           |
| ----------------------- | ---------------------------------------------------- |
| **URL endpoint (POST)** | https://app.senangpay.my/apiv1/update\_token\_status |



### **2.1 Authorization header (Basic Auth)**

| Type     | Basic                                                                       |
| -------- | --------------------------------------------------------------------------- |
| Username | <p>&#x3C; your-merchant-id ><br>As listed in the profile settings page.</p> |
| Password | None, leave empty.                                                          |



### **2.2 Request Parameter (All Mandatory)**

| Parameter Name | Parameter value / description                                            |
| -------------- | ------------------------------------------------------------------------ |
| token          | Generated token from [Get Token API](3d-get-token.md#integration-method) |



### **2.3 Response Parameter**

| **Parameter Name** | **Parameter value/description**                                       |
| ------------------ | --------------------------------------------------------------------- |
| msg                | Message for the token is successfully disabled or enabled.            |
| token              | Generated token from Get Token API that has been disabled or enabled. |



{% swagger src="../../.gitbook/assets/swagger phase 1_update code.yaml" path="/apiv1/update_token_status" method="post" %}
[swagger phase 1_update code.yaml](<../../.gitbook/assets/swagger phase 1_update code.yaml>)
{% endswagger %}

###

### **3.0 Validate payment token**

| **Item**                | **Detail**                                     |
| ----------------------- | ---------------------------------------------- |
| **URL endpoint (POST)** | https://app.senangpay.my/apiv1/validate\_token |



### **3.1 Authorization header (Basic Auth)**

| Type     | Basic                                                                       |
| -------- | --------------------------------------------------------------------------- |
| Username | <p>&#x3C; your-merchant-id ><br>As listed in the profile settings page.</p> |
| Password | None, leave empty.                                                          |

### **3.2 Request Parameter (All Mandatory)**

| Parameter Name | Parameter value / description                                            |
| -------------- | ------------------------------------------------------------------------ |
| token          | Generated token from [Get Token API](3d-get-token.md#integration-method) |

&#x20;

### **3.3 Response Parameter**

<table data-header-hidden><thead><tr><th width="223"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter Name</strong></td><td><strong>Parameter value/description</strong></td></tr><tr><td>status</td><td><p>Token validation result. </p><ul><li><code>1</code> for success</li><li><code>0</code> for failure.</li></ul></td></tr><tr><td>msg</td><td>Message on token validation. "<strong>Card has been successfully verified</strong>" if successful, or an error message if not.</td></tr><tr><td>token</td><td>The token from the <em>Get Token API,</em> unchanged, showing whether it's enabled or disabled.</td></tr></tbody></table>



{% swagger src="../../.gitbook/assets/swagger phase 1_update code.yaml" path="/apiv1/validate_token" method="post" %}
[swagger phase 1_update code.yaml](<../../.gitbook/assets/swagger phase 1_update code.yaml>)
{% endswagger %}



[^1]: 
