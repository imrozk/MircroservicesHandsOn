---
layout: "post"
title: "Order"
date: "2020-11-08 14:24"
---

# Order
Order is the root agregate for the Payment context it is the  first entity created to initate a payment.

An order helps us in binding the product bought with the payment it also helps us in preventing multiple payments as an order can be paid only once and no payment can be initiated until even a single payment is in progres.

The order Entity can go through following states:
1. CREATED
2. PAYMENT_ATTEMTED
3. PAID

The state diagram for order is as below:
![State transition Diagram](/images/2020/11/stateDiagram.png)
________________________________
yUML syntax for state transition:
```yuml:activity:scruffy
(start)->(CREATED)
(CREATED)->[Initiate Payment]->(PAYMENT_ATTEMTED)
(PAYMENT_ATTEMTED)-><a>
<a>->[Success]->(PAID)
<a>->[Payment failed]->(CREATED)
(PAID)->(end)
```
_________________________________

### Attributes
Following are the attributes associated to the Order entity

| Attribute | Type        | Description |Access  |
| --------- | ----------- |------------ |------- |
| _OrderKey_  | Number | Primary Identifier  for Order | Read Only |
| _Merchant_  | Number  | Identifier for the merchant for whome the order is created. |  Read/Write |
| _Ammount_ | Number | Ammount for which order is generate, this id a mnadatory field for order generation | Read/Write |
| _amountBreakup_   | Number   | Breakup for the ammount to be paid.  | Read/Write  |
| _amountPaid_   | Number | Read only field to be used for reconciliation on order level, in v1 no partial payment is allowed.  | Read Only  |
| _amountDue_ | Nummber |  Read only field to be used for reconciliation at order level. | Read Only |
| _status_  | string | Status of the order.  |  Read Only |
| _attempts_  | Number  |  number of payment attemps for the order. | Read Only  |
| _createdAt_  | date  | Time at which order is created.  | Read Only  |
| _products_  | List<Product>  |  List of products the order is created for | Read/Write  |
|  _eligiblePaymentChannels_ | List<PaymentChannels>  |  List of Paymentment channels the order is eligible for. | Read Only  |
| _merchantTransactionRef_ | string  | This is a weak entity and will be used to identify the merchants transaction in the payment domain.  <br> Payment domain will not handle the lifecycle of this entity and the same should be managed at the partner end.   | Read/Write  |
| notes  | string  | any additional info to be sent with order, this can be a key value pair and will be reflected in the payment entities for this order.   | Read/Write |
