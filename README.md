# Stripe Event Types

[![npm](https://img.shields.io/npm/v/stripe-event-types)](https://www.npmjs.com/package/stripe-event-types)
[![Build](https://github.com/kgajera/stripe-event-types/actions/workflows/build.yml/badge.svg)](https://github.com/kgajera/stripe-event-types/actions/workflows/build.yml)

This provides TypeScript typings for Stripe webhook events to strongly type the `type` and `data.object` fields. These types are automatically generated by scraping Stripe's documentation for [types of events](https://stripe.com/docs/api/events/types).

Why is this needed? The typings included in the [`stripe`](https://github.com/stripe/stripe-node) library are lacking in this respect. The type for `type` is a `string` instead of a string literal and the type for `data.object` is `{}` which requires casting each usage of it. This can lead to mistakes in your implementation that could easily be caught with stronger types.

![Typed Webhook Event](https://user-images.githubusercontent.com/1087679/187047509-d8cfe324-0e19-468e-8cdf-7fd3f503ad1f.gif)

## Installation

Install the package with:

```shell
npm install stripe-event-types
# or
yarn add stripe-event-types
```

### Version compatability

| `stripe-event-types` version | `stripe` version |
| ---------------------------- | ---------------- |
| 2                            | 11               |
| 1                            | 10               |

## Usage

### Webhook event

When constructing the webhook event, cast it to `Stripe.DiscriminatedEvent` to strongly type the `type` and `data.object` fields:

```diff
+/// <reference types="stripe-event-types" />

const event = stripe.webhooks.constructEvent(
  request.body,
  request.headers['stripe-signature'],
  'whsec_test'
-);
+) as Stripe.DiscriminatedEvent;
```

### Event type

The `Stripe.DiscriminatedEvent.Type` type is a string literal of all event types:

```ts
/// <reference types="stripe-event-types" />

const type: Stripe.DiscriminatedEvent.Type = "charge.succeeded";
```
