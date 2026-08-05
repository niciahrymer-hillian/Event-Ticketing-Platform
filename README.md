# Event-Ticketing-Platform

### Ticketing platform: seat holds and time-limited reservations with no double-booking under load.

![Chain O](https://img.shields.io/badge/Chain%20O-D97706?style=for-the-badge) [![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue?style=for-the-badge)](LICENSE-GPL) [![License: AGPL v3](https://img.shields.io/badge/License-AGPLv3-blue?style=for-the-badge)](LICENSE-AGPL)

[📖 Lesson Plan](docs/LESSON_PLAN.md)

<!-- SCREENSHOT PLACEHOLDER: docs/screenshots/overview.png -->

> ⬜ **Scaffold pending.** Directory created to portfolio standard; full content (README, lesson plan, tour + quiz, skeleton code) to be built. Part of **Chain O — System Design & Architecture**.

## Why This Was Built

Ticketing is the cleanest possible demonstration of a concurrency problem: many people want the same seat
at the same instant, and selling it twice is unacceptable. There is no way to hand-wave this — either the
database guarantees it or your system is broken.

I've already dealt with a version of this in my Chain G work, where two applicants can compete for the same
unit and the guarantee has to live in the database rather than in application code. Ticketing is the same
problem with a harder deadline, plus time-limited holds that must expire reliably.

## Why This Matters (Industry Application)

Concurrency correctness is one of the highest-signal things an engineer can demonstrate. Inventory,
booking, reservations, and payments all share this shape, and the tools — row locks, optimistic concurrency,
unique constraints, transactional boundaries — are the same everywhere. Getting it right under load is a
genuine differentiator.

## Topics Covered

| Area | What this project covers |
|------|--------------------------|
| Double-booking | Guaranteeing a seat is sold exactly once |
| Holds | Time-limited reservations and reliable expiry |
| Locking | Pessimistic row locks vs optimistic concurrency |
| DB guarantees | Constraints that hold even when app logic is wrong |
| Load | Behavior under a spike when a popular event opens |
| Payment coupling | Releasing a hold when payment fails |

## How This Connects

Chain O (System Design & Architecture). Same concurrency guarantee as the unit-application rule in my Chain G work; uses **Caching-And-Queues** for hold expiry.

---
Dual licensed — [GPL v3](LICENSE-GPL) and [AGPL v3](LICENSE-AGPL).
