---
layout: post
title: Domain Model
date: '2020-11-08 14:23'
---

# Domain Model

Below is the Domain model defining the Payments domain:

![Domian Model](/images/2020/11/DomainModel.png)
_____________
The domain entities work on the  following rule:
1. **Order** is the root agregate
2. Single order can have multiple Payments.
3. Only 1 **Payment** can be In-progress or completed at a time for an order.
4. To **create a new payment** for an order, Order must be in created state, and no other payment should be in active, in progress or Completed.
5. **Product** is a weak entity, i.e. management of product will not be handled by the Payment domain, it will be used to acertain payment channel eligibility and display.
6. **Payment Instrument** is the method used for payment, e.g. _Credit card_, _Debit Card_, _UPI_ etc.
7. **Payment Provider** is the payment gateway or provider through which we are processing the payment.
8. **Payment channel** is a combination of Payment Instrument and payment provider, it uniquely identifies the payment machanism.
_____________
