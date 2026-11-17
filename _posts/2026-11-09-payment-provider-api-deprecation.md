---
title: "The Email You Didn't Want: Your Payment Provider Is Retiring Its API"
description: "Your checkout works today and breaks on a date someone else chose. Why providers retire APIs, how to size up your exposure, and how to stop owning the work."
date: 2026-11-09
tags: [payments, orchestration]
hero: /assets/images/blog/payment-provider-api-deprecation.jpg
image: /assets/images/og/blog/payment-provider-api-deprecation.jpg
image_alt: "A deprecation notice with a countdown, sitting between a working checkout and a broken one"
# Held back until the two images above exist in assets/images/blog/ and assets/images/og/blog/.
# Without them the post would publish with a broken hero and a broken social card.
# Delete this line when they are in place.
published: false
related:
  - /blog/switch-payment-providers-without-losing-sales/
  - /blog/payment-integration/
  - /blog/single-payment-processor-limitations/
---

It arrives on an ordinary Tuesday, with a subject line calm enough to ignore:
"Important changes to our API." Three paragraphs down is the part that
matters. The API version your integration uses will stop accepting requests in
ninety days. There is a migration guide. There is a support address. There is
no option to decline.

Your checkout works perfectly today. It stops working on a date somebody else
chose, and you didn't change a thing. This isn't a bug you introduced or a
decision you made badly. It's maintenance work handed to you with a deadline
attached, in a quarter that was already full.

## Why it happens

- **Providers deprecate for reasons that are usually legitimate.** Old
  authentication schemes, weak signature algorithms and pre-SCA flows all have
  to go eventually. The provider isn't being careless with your time; it's
  retiring something it can no longer defend keeping alive.
- **Card scheme and regulatory mandates cascade downwards.** When the networks
  or a regulator set a deadline, your provider is a middle link in that chain,
  not the origin of it. They pass the date along because they received it too.
- **Acquisitions force platform migrations.** A provider gets bought and the
  acquirer moves everyone onto its own stack. The API you integrated against
  was never the long-term plan; you weren't told that at the time.
- **Your plugin is frozen at the version it shipped with.** A cart or billing
  plugin is pinned to whatever API existed when it was written. If the author
  has moved on, nobody is preparing an update, and the notice period quietly
  becomes your development schedule.
- **"Upgrade the version" is rarely one change.** A deprecation usually bundles
  a new credential format, renamed fields, different webhook signing, and
  changed status values. It's a re-integration wearing a smaller word, and
  ninety days is brutal if your integration was written once, two years ago, by
  a contractor who is no longer available.

## How to diagnose your exposure

- **Establish which API version you are actually on**, not which one the
  documentation currently shows. Check the endpoint path and version header
  your integration sends. Plugin settings screens almost never surface this,
  and assumptions here are where migrations go wrong.
- **Read the migration guide for breaking changes specifically.** Skip the
  changelog prose and hunt for four things: credential or authentication
  changes, webhook signature changes, removed or renamed fields, and changed
  status or error values. Those four account for most of the real work.
- **Check whether the plugin or library you rely on is still maintained.** Look
  at the last release date and whether anyone has raised the deprecation. An
  unmaintained plugin means the work is yours, whether or not you wrote the
  original code.
- **Inventory everything that touches the provider, not just checkout.**
  Refunds, recurring billing, reconciliation exports and webhook handlers are
  all separate surfaces, and the forgotten one is usually refunds.
- **Rebuild against the new version in sandbox before you commit to a date.**
  Sandbox parity is imperfect, but an afternoon there tells you whether you're
  facing a config change or a fortnight of work.
- **Confirm the real cut-off.** Providers often stop supporting a version
  before they block it, and sometimes enforce earlier for newer accounts. The
  date in the email isn't always yours.

## How to fix it

- **Start before the final fortnight.** Payment migrations slip for ordinary
  reasons: a webhook edge case, a sandbox gap, someone on leave. Provider and
  scheme deadlines don't slip to accommodate any of that.
- **Migrate and redesign separately.** The temptation to improve the checkout
  while you're in there is strong and reliably costly. Get to parity on the new
  version first, then change behaviour deliberately.
- **Run both versions in parallel if the provider allows it.** Send a slice of
  traffic through the new integration and compare approval rates, webhook
  delivery and refund behaviour against the old one before switching fully.
- **Re-test the entire money path**, including a real refund and at least one
  recurring charge. A migration that passes checkout and fails refunds is worse
  than one that fails loudly on day one.
- **Keep a rollback until the old version is genuinely blocked.** While it
  still answers requests, being able to revert turns a bad deploy into an
  inconvenience rather than an outage.
- **Treat the notice as a question about architecture.** If one provider's
  release notes can set an expiry date on your checkout, the deprecation is the
  symptom and a single hard-wired integration is the finding.

## How InfyniPay addresses this

InfyniPay is a [payment orchestration
platform](/blog/what-is-payment-orchestration/) that sits between your store
and {{ site.provider_floor }} payment providers. You integrate with InfyniPay
once; InfyniPay maintains the integrations on the provider side. When a
provider changes or retires an API version, that work happens on our side of
the line rather than in your checkout code or a cart plugin you don't control.

It's worth being precise about what this does and doesn't cover. Your provider
accounts and contracts remain yours, so anything the provider needs directly
from you (rotated credentials, a new compliance attestation, updated KYC)
still comes to you, and a provider that retires a product altogether has still
retired it. What changes is who writes the migration code, and whether a single
provider's deadline means a broken checkout or a routing change.

## Where InfyniPay fits

If your checkout's expiry date is set by somebody else's release notes, the
underlying problem isn't the deprecation. It's having exactly one integration
to lose. InfyniPay connects your store to {{ site.provider_floor }} providers
through one free integration, with routing, failover and webhook verification
built in, and **no per-transaction fee** from InfyniPay at any volume. Free
plugins are available for [WHMCS](/integrations/whmcs/) and
[WooCommerce](/integrations/woocommerce/) alongside the other major carts and
billing systems.

[Create a free InfyniPay account]({{ site.signup_url }}), or browse the
[provider directory](/providers.html) to see which alternatives you could route
to if the deadline arrives before your migration is ready.
