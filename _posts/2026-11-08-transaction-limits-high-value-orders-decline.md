---
title: "The Limit Nobody Told You About: Why Your Highest-Value Order Won't Go Through"
description: "A big order gets rejected with no decline code at all. Why payment providers cap transaction size, how to spot the ceiling, and how to stop losing your best sales."
date: 2026-11-08
tags: [payments, orchestration]
hero: /assets/images/blog/transaction-limits-high-value-orders-decline.jpg
image: /assets/images/og/blog/transaction-limits-high-value-orders-decline.jpg
image_alt: "A large order total hitting an invisible ceiling instead of reaching the card network"
# Held back until the two images above exist in assets/images/blog/ and assets/images/og/blog/.
# Without them the post would publish with a broken hero and a broken social card.
# Delete this line when they are in place.
published: false
related:
  - /blog/how-to-improve-your-payment-approval-rate/
  - /blog/payment-account-hold-rolling-reserve/
  - /blog/single-payment-processor-limitations/
---

A corporate client wants to pay a five-figure invoice by card instead of wiring
the money, which should be good news: card payments settle faster and need no
manual reconciliation. They enter the card, hit pay, and get rejected
immediately, before the request even seems to reach their bank. No decline
code, no "insufficient funds," nothing you can explain to them except "try
again" or "wire it instead." Your biggest order of the quarter has just become
your slowest one.

The card is fine. The customer is fine. The thing that failed is a number you
have probably never seen, sitting on your own account rather than theirs.

## Why it happens

- **Most providers cap a single transaction, by default, well below what a
  card is actually capable of.** New or lower-tier accounts especially get a
  conservative ceiling set at onboarding, a figure that has nothing to do
  with the cardholder's own limit and everything to do with the provider's
  risk appetite for an account with no processing history yet.
- **The cap is account-level, not card-level, so it rejects before the network
  is even asked.** This is why there's no normal decline code: the transaction
  never reaches the issuer. Your provider's API returns a generic rejection,
  and support may be the only place willing to actually state the number.
- **Limits are set to match your typical order size, and your typical order
  size is what the provider expects to keep seeing.** A merchant whose average
  sale is small gets a risk profile built around small orders; a one-off
  high-value invoice looks nothing like the account's history, which is
  exactly the kind of outlier a risk model exists to catch.
- **Raising it isn't instant.** Most providers will lift a transaction limit
  on request, but that's a support ticket and a review, not a dashboard
  toggle, and it rarely resolves before the customer currently sitting at your
  checkout has given up and gone elsewhere.
- **It looks identical to a card problem.** A flat rejection with no code
  reads to the customer (and often to your own support team) exactly like
  something wrong with their card, which sends everyone diagnosing the wrong
  layer entirely.

## How to diagnose it

- **Check whether the failure happened before or after the request reached
  the card network.** A provider-side cap rejects instantly and silently; a
  genuine issuer decline comes back with a code, even a vague one like "do not
  honour."
- **Compare the order value against your account's typical range.** If every
  failed high-value order clusters above a specific amount and every smaller
  order clears fine below it, that threshold is very likely your transaction
  cap, not a coincidence.
- **Ask the provider directly what your current per-transaction and daily
  limits actually are.** Most dashboards don't surface this number anywhere a
  merchant would think to look; it usually takes a direct support request to
  get a straight answer.
- **Test the same order amount through a second provider, if you have one.**
  A limit specific to one account clears immediately through a different one
  with nothing else about the transaction changed.

## How to fix it

- **Ask for a limit increase before you need it, not during the sale.** If a
  product line, an invoice tier, or a seasonal push routinely produces orders
  above your current cap, request the increase as soon as you can see it
  coming, not after the first customer hits the wall.
- **Route high-ticket orders to whichever connected provider already has the
  higher ceiling.** If one provider has raised your limit and another hasn't,
  the fix for a given order is which account processes it, not a
  renegotiation with the one that just rejected it.
- **Don't let your historical order profile become a permanent ceiling.** An
  account that has processed nothing but modest orders for a year will keep
  defaulting to a modest-order limit until someone explicitly asks for more,
  even once the business has clearly grown past it.
- **Give the customer a working alternative in the moment**, not just an
  apology. A bank transfer option or a second card field buys you the sale
  while the limit increase is still sitting in someone's review queue.

## How InfyniPay addresses this

InfyniPay doesn't set or raise transaction limits. Those stay between you
and each provider, since you keep your own account and your own contract with
every one you connect. What changes is that a limit on one account doesn't
become a limit on the business. Because InfyniPay is a
[payment orchestration platform](/blog/what-is-payment-orchestration/) sitting
in front of {{ site.provider_floor }} providers, you can route your
highest-value orders to whichever connected provider already has the ceiling
they need, rather than discovering the cap for the first time when a real
customer hits it.

## Where InfyniPay fits

If your biggest sales are the ones most likely to fail, the cause is more
often a transaction cap than a card problem, and the fix is having more than
one ceiling to route around. InfyniPay connects your store to
{{ site.provider_floor }} providers through one free integration, with
routing, failover and webhook verification built in, and **no per-transaction
fee** from InfyniPay at any volume. Free plugins are available for
[WooCommerce](/integrations/woocommerce/) and [WHMCS](/integrations/whmcs/)
alongside the other major carts and billing systems.

[Create a free InfyniPay account]({{ site.signup_url }}), or browse the
[provider directory](/providers.html) to compare transaction limits before
your next high-value order is the one that tests them.
