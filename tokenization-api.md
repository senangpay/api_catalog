---
icon: key
---

# Tokenization API

Allows merchant to charge customer’s credit card without the need to enter the credit card details (name, card number, expiry and cvv). To get this feature in your dashboard, you can notify us by sending a ticket from the dashboard or guide page. This application shall be subjected to senangPay approval which we will review at our own discretion. Merchant must provide us the **Terms of Contract** between merchant and the other party user.



## **How does it works?**

Merchant’s customers will enter their credit card details one time only. During this one time process, senangPay will validate the card to make sure the card is valid by charging an amount of RM1 to the card. Not to worry that this amount will be voided later. Meaning that the transaction will never appeared on the customer’s credit card statement.

If senangPay failed to charge the card, meaning that the card is not valid. Once validated, the card’s info will be stored in senangPay’s server (PCI-DSS certified).



***

## API List

We have developed a new secure way of generating token for our tokenization payment. In this new feature, card holder is required to pass the OTP (3D secure) check before able to get the payment token. Also, there are few extra layers been added to ensure no non authorised card being used for this tokenization payment feature.



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

<table data-header-hidden><thead><tr><th width="258"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter Name</strong></td><td><strong>Parameter value/description</strong></td></tr><tr><td>name</td><td>Your customer name. Maximum length is 100.<br>Eg. Abu Bin Ali</td></tr><tr><td>email</td><td>Your customer email.<br>Eg. ahmad@google.com</td></tr><tr><td>detail</td><td>Your order detail. Maximum length is 100. Eg. Order for product id #4</td></tr><tr><td>phone</td><td>Your customer phone number.<br>Eg. 0109876543</td></tr><tr><td>order_id</td><td>Your order id. Can be number or string. Other character is invalid. Eg. 123</td></tr><tr><td>amount</td><td>Your order amount in integer format. Convert from decimals as necessary.<br>Eg. if the amount is RM 2.00, you need to send 200.</td></tr><tr><td>token</td><td>Generated token from Get Token API</td></tr><tr><td>hash</td><td>A string hashed with your secret key (from your profile setting page) in HMAC hashing algorithm with SHA256 in the following format:<br>&#x3C; your merchant id >&#x3C; name >&#x3C; email >&#x3C; phone >&#x3C; detail >&#x3C; order_id >&#x3C; amount ><br>*without the &#x3C; > character</td></tr></tbody></table>



### **1.3 Response Parameter**

<table data-header-hidden><thead><tr><th width="247"></th><th></th></tr></thead><tbody><tr><td>Parameter Name</td><td><strong>Parameter value / description</strong></td></tr><tr><td>status</td><td>Your transaction status. 1 if successful. 0 if failed.</td></tr><tr><td>transaction_id</td><td>Your transaction ID number.</td></tr><tr><td>order_id</td><td>Your original order ID.</td></tr><tr><td>amount_paid</td><td>Amount transacted from the credit card in integer format.<br>E.g., if the amount transacted is RM 2.00, it will output 200.</td></tr><tr><td>msg</td><td>Transaction status message. If it was successful you will receive ‘Payment was successful’. If the transaction failed, you will receive the error message in this parameter for further checking.</td></tr><tr><td>hash</td><td><p>A string hashed with your secret key (from your profile setting page) in HMAC hashing algorithm with SHA256 in the following format:</p><p>&#x3C; your merchant id >&#x3C; status_id >&#x3C; order_id >&#x3C; transaction_id >&#x3C; amount_paid >&#x3C; msg ></p><p>*without the &#x3C;  > character</p></td></tr></tbody></table>

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

| Parameter Name | Parameter value / description      |
| -------------- | ---------------------------------- |
| token          | Generated token from Get Token API |



### **2.3 Response Parameter**

| **Parameter Name** | **Parameter value/description**                                       |
| ------------------ | --------------------------------------------------------------------- |
| msg                | Message for the token is successfully disabled or enabled.            |
| token              | Generated token from Get Token API that has been disabled or enabled. |





### **3.0 Validate payment token**

| **Item**                | **Detail**                                     |
| ----------------------- | ---------------------------------------------- |
| **URL endpoint (POST)** | https://app.senangpay.my/apiv1/validate\_token |



### **3.1 Authorization header (Basic Auth)**

| Type     | Basic                                                                       |
| -------- | --------------------------------------------------------------------------- |
| Username | <p>&#x3C; your-merchant-id ><br>As listed in the profile settings page.</p> |
| Password | None, leave empty.                                                          |

###

### **3.2 Request Parameter (All Mandatory)**

| Parameter Name | Parameter value / description      |
| -------------- | ---------------------------------- |
| token          | Generated token from Get Token API |

&#x20;

### **3.3 Response Parameter**

<table data-header-hidden><thead><tr><th width="223"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter Name</strong></td><td><strong>Parameter value/description</strong></td></tr><tr><td>status</td><td>Token validation status. 1 if success. 0 if failed.</td></tr><tr><td>msg</td><td>Token validation status message. If it was successful you will receive ‘Card has been successfully verified.’. If the validation failed, you will receive the error message in this parameter for further checking.</td></tr><tr><td>token</td><td>Generated token from Get Token API that has been disabled or enabled. The token will still be the same, nothing changed. We just return the same token here.</td></tr></tbody></table>
