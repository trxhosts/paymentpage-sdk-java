[![Build Status](https://travis-ci.com/trxhosts/paymentpage-sdk-java.svg?branch=main)](https://travis-ci.com/trxhosts/paymentpage-sdk-java)

# TrxHosts payment page SDK

This is a set of libraries in the Java language to ease integration of your service
with the TrxHosts Payment Page.

## Payment flow

![Payment flow](flow.png)

### Get URL for payment

```java
Gate gate = new Gate("secret");
Payment payment = new Payment("11");

payment
    .setParam(Payment.PAYMENT_ID, "some payment id")
    .setParam(Payment.PAYMENT_AMOUNT, 1001)
    .setParam(Payment.PAYMENT_CURRENCY, "EUR");

String paymentUrl = gate.getPurchasePaymentPageUrl(payment);
``` 

`paymentUrl` here is the signed URL.

### Handle callback from TrxHosts

You'll need to autoload this code in order to handle notifications:

```java
Gate gate = new Gate("secret");
Callback callback = gate.handleCallback(callbackData);
```

`data` is the JSON string received from payment system;

`callback` is the Callback object describing properties received from payment system;
`callback` implements these methods: 
1. `callback.getPaymentStatus();`
    Get payment status.
2. `callback.getPayment();`
    Get all payment data.
3. `callback.getPaymentId();`
    Get payment ID in your system.
