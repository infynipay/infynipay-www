---
title: "When Your Chargeback Ratio Crosses the Line: Visa and Mastercard Monitoring Programmes, Explained"
description: "A handful of extra disputes tips your chargeback ratio over a card network threshold, and suddenly you're in a monitoring programme, or losing the account."
date: 2026-11-15
tags: [payments, orchestration]
hero: /assets/images/blog/chargeback-ratio-monitoring-programs.jpg
image: /assets/images/og/blog/chargeback-ratio-monitoring-programs.jpg
image_alt: "A chargeback ratio gauge climbing past a red threshold line toward a frozen account icon"
# Held back until the two images above exist in assets/images/blog/ and assets/images/og/blog/.
# Without them the post would publish with a broken hero and a broken social card.
# Delete this line when they are in place.
published: false
related:
  - /blog/chargebacks-across-multiple-payment-providers/
  - /blog/payment-account-hold-rolling-reserve/
  - /blog/single-payment-processor-limitations/
---

Nothing about last month felt unusual. Sales were up slightly, the product
hadn't changed, and the handful of chargebacks that came in looked like the
usual mix of "didn't recognise the charge" and "never received the item." Then
an email arrives from your payment provider's risk team: your account has been
enrolled in a card network chargeback monitoring programme. You have a
deadline to bring the ratio down, a fee attached to every month you don't, and
a clear statement that continued non-compliance ends in account termination.

Nobody told you the number you needed to watch, or where the line was, until
you'd already crossed it.

## Why it happens

- **Visa and Mastercard both run ratio-based monitoring programmes**, commonly
  known by names like Visa's Dispute Monitoring Programme and Mastercard's
  Excessive Chargeback Programme. Each measures chargebacks as a percentage of
  your transaction count in a rolling window, usually a calendar month, at a
  **specific threshold**, often cited around 0.9%–1% for standard monitoring
  and higher tiers for persistent breaches.
- **The ratio is per merchant account (MID), not per business.** If you
  process through one provider, every dispute on every sale counts against
  one small denominator. A slow month with fewer total transactions makes the
  same handful of chargebacks a much bigger percentage, even if the dispute
  count itself didn't change.
- **A single bad batch can push you over.** A delayed shipment, a product
  defect, a fraud attack that got through, or simply a smaller sales month:
  any of these can move the ratio from comfortable to breached without a
  change in the underlying rate of genuine problems.
- **Your provider often enrols you before you see a network notice.** The card
  schemes set the threshold, but it's the acquirer or PSP that monitors it and
  passes on the programme fees, the reporting burden and the compliance
  deadline, sometimes with little warning, because they're passing along a
  deadline they didn't set either.
- **Fees stack while you're in the programme**, independent of whatever the
  original disputes already cost you in lost goods and chargeback fees. Being
  enrolled is itself a recurring cost, and it compounds for every month the
  ratio stays over the line.

## How to diagnose it

- **Ask your provider for the exact ratio and the exact threshold**, not just
  the fact that you've been enrolled. "Chargeback ratio" calculations vary
  slightly by network and programme tier, and you need your real number to
  know how far over you are and how much movement would clear it.
- **Pull the chargeback list behind the number.** Group disputes by reason
  code. Fraud-coded disputes, "product not received," and "not as described"
  each point to a different fix; treating them as one undifferentiated
  problem wastes the time you have before the next reporting cycle.
- **Check whether the breach is a rate problem or a volume problem.** If your
  chargeback count has been flat but total transactions dropped, the ratio
  moved because the denominator shrank. That is a different situation than an actual
  increase in disputes, and one that resolves differently.
- **Look at concentration by product, country or campaign.** Monitoring
  programmes react to the account-wide ratio, but the drivers are rarely
  evenly spread; a single SKU or traffic source is often responsible for a
  disproportionate share.

## How to fix it

- **Respond to every dispute you can genuinely contest, with evidence,
  before the deadline.** A won dispute can sometimes be excluded from the
  ratio depending on programme rules; even where it isn't, fighting winnable
  cases keeps the underlying rate from climbing further.
- **Fix the reason code, not just the symptom.** "Product not received" means
  shipping and tracking need attention; "not as described" means your product
  pages or expectations-setting need attention; a fraud-coded cluster means
  your checkout's fraud controls need attention. Each has a different owner.
- **Tighten the controls that stop disputes before they start**: clearer
  billing descriptors, proactive order confirmation and shipping emails, an
  easy-to-find refund policy, and a visible way to contact support before a
  customer's next move is calling their bank instead of you.
- **Increase total transaction volume where you honestly can, rather than
  suppressing orders you'd otherwise take.** Because the ratio is a
  percentage, legitimate volume genuinely dilutes it, but only alongside a
  falling dispute count, not as a substitute for one.
- **Know what happens if you don't clear it in time.** Programmes typically
  escalate in tiers, with rising fees, before the network or acquirer can
  terminate the account outright. Understand your specific provider's
  timeline now, while you still have one.

## How InfyniPay addresses this

InfyniPay doesn't change how Visa or Mastercard calculate a chargeback
ratio, and it can't negotiate you out of a programme you're already enrolled
in. That relationship sits between you and the provider that holds your
merchant account. What changes is the exposure a single enrolment represents.
Because InfyniPay is a [payment orchestration
platform](/blog/what-is-payment-orchestration/) sitting in front of
{{ site.provider_floor }} providers, your sales volume isn't locked to one
MID with one ratio to breach. If one provider enrols you in monitoring or
moves toward terminating the account, you still have other connected
providers processing live traffic rather than a checkout that stops taking
payments the day the first one does.

It also makes the diagnosis easier. Disputes and transaction counts across
every connected provider land in one place instead of several dashboards, so
spotting which product, country or campaign is actually driving the ratio
doesn't require logging into each provider separately and reconciling the
numbers by hand.

## Where InfyniPay fits

A chargeback ratio breach is a genuine compliance problem that only you and
your provider can fix, but a single merchant account being the entire
business is what turns that breach into an existential one. InfyniPay
connects your store to {{ site.provider_floor }} providers through one free
integration, with routing, failover and webhook verification built in, and
**no per-transaction fee** from InfyniPay at any volume. Free plugins are
available for [WHMCS](/integrations/whmcs/) and
[WooCommerce](/integrations/woocommerce/) alongside the other major carts and
billing systems.

[Create a free InfyniPay account]({{ site.signup_url }}), or browse the
[provider directory](/providers.html) to line up a second provider before a
ratio breach on your only one becomes a reason to stop trading.
