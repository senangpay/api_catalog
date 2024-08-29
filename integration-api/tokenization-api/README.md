---
icon: key
---

# Tokenization API

This feature lets merchants charge a customer’s credit card without needing to manually enter card details (such as the card number, expiration date, or CVV). To enable this feature on your dashboard, please submit a request through the ticket system available in the dashboard or guide page. Approval for this feature is at senangPay's discretion, and we will review your request accordingly. Additionally, merchants must provide the Terms of Contract between themselves and the user for our review.



## **How does it works?**

Customers will need to enter their credit card details only once. During this process, senangPay will validate the card by charging a temporary amount of RM1. Rest assured, this charge will be promptly voided and will not appear on the customer’s credit card statement.

If senangPay is unable to process this charge, it indicates that the card is invalid. Once the card is successfully validated, its information will be securely stored on senangPay’s PCI-DSS certified servers.



## Elevating Security: New OTP Verification and Enhanced Measures for Tokenization Protection

We are excited to introduce an enhanced, secure method for generating tokens for our tokenization payment system. This new feature adds an additional layer of security by requiring cardholders to complete an OTP (3D Secure) verification before they can obtain a payment token.

Additionally, we've implemented several extra security measures to ensure that only authorized cards are used for tokenization. These improvements are designed to safeguard against unauthorized use and further protect your transactions.



<figure><img src="../../.gitbook/assets/flow-02.png" alt=""><figcaption><p>Token Generation Flow: From Token Creation to Payment Card Use and Callback Confirmation</p></figcaption></figure>



***





{% content-ref url="3d-get-token.md" %}
[3d-get-token.md](3d-get-token.md)
{% endcontent-ref %}

{% content-ref url="tokenization-api-list.md" %}
[tokenization-api-list.md](tokenization-api-list.md)
{% endcontent-ref %}

