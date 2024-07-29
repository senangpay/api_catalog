---
description: testing page from gitbook edit
---

# Integration API

If you have develop your own shopping cart and need manual integration by yourself, here are the details.

**1. Info required(test)**

To start we will need the information as below. These can be retrieve in senangPay Dashboard.

1.1 Go to Menu > Settings > Profile

1.2 Refer to **Shopping Cart Integration Link** section. Get your **Merchant ID** and **Secret Key** information.

1.3 Then you will need to fill in the return URL. This is the URL where senangPay will redirect the buyer after the payment has been processed.

1.4 Next, you need to fill the Callback URL. Callback URL is used as alternative notification to merchant shopping cart in case there is a breakdown in transaction flow. For more info on Callback URL, read [here](https://guide.senangpay.my/callback-url/)

**2. What parameters to send to senangPay**

Below are the details of the elements in the table :

