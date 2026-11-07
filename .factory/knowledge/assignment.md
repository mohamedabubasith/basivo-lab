---
title: How users are assigned to variants
summary: MurmurHash3 32-bit seed 0 of "<experimentKey>:<userId>" mod 10000 picks the variant; a separate "<key>:traffic:<userId>" mod 100 hash decides inclusion. Server and SDK must share one implementation.
reviewed: 2026-11-08
---
# Variant assignment

The most important rule in the product: a user must always get the same variant, on every server and in the SDK.

- Variant bucket: MurmurHash3 (x86, 32-bit, seed 0) of the UTF-8 string `"<experimentKey>:<userId>"`, as an unsigned integer, modulo 10000
- Variants own consecutive bucket ranges in their configured order, sized by weight (weight 50 = 5000 buckets). The first variant is the control
- Traffic inclusion (gradual rollout): MurmurHash3 of `"<experimentKey>:traffic:<userId>"` modulo 100, included when below `traffic`. It is a separate hash so raising traffic never changes anyone's variant
- Assignment is a pure function with no database access. The server and the JavaScript SDK import the same module
- Once a user is exposed, events are attributed to the stored variant, never recomputed
