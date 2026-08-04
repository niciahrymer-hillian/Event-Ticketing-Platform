# 📖 Lesson Plan — Event-Ticketing-Platform

> **Chain O — System Design & Architecture** | Ticketing platform: seat holds and time-limited reservations with no double-booking under load.

## What This Project Is

Build a ticketing service where selling the same seat twice is unacceptable, and put the guarantee in the database rather than in hopeful application logic.

## Learning Objectives

By the end I can:

1. Model seats, holds, and orders with the correct constraints.
2. Guarantee at the **database level** that a seat is sold at most once.
3. Compare pessimistic row locking with optimistic concurrency.
4. Implement **time-limited holds** that expire reliably.
5. Release a hold correctly when payment fails or times out.
6. Demonstrate correctness under concurrent load.

## Software You Will Use

- Python/FastAPI or Java/Spring.
- PostgreSQL for transactional guarantees.
- Redis or a scheduled job for hold expiry.
- A concurrency test harness.

## Build Order

1. Model the schema; add a unique constraint that makes double-selling impossible.
2. Implement seat selection with `SELECT ... FOR UPDATE`.
3. Write a concurrency test that hammers one seat with many buyers.
4. Implement holds with an expiry, and a reaper that releases them.
5. Wire payment; release the hold on failure.
6. Re-run the concurrency test and prove the invariant holds.

## Common Mistakes to Avoid

- Checking availability and then inserting, with no lock in between.
- Enforcing the invariant only in application code, so any other writer breaks it.
- Holds that never expire because the reaper silently died.
- Long transactions held open across a payment call.
- Testing only sequentially and never under real concurrency.

## Check Your Understanding

The quiz covers why check-then-insert races, pessimistic vs optimistic locking, and why the database must own the invariant.

## Why This Matters (Industry Application)

Concurrency correctness is one of the highest-signal things an engineer can demonstrate. Inventory,
booking, reservations, and payments all share this shape, and the tools — row locks, optimistic concurrency,
unique constraints, transactional boundaries — are the same everywhere. Getting it right under load is a
genuine differentiator.

## Reflection Questions

- How long should a hold last — and who bears the cost if it is too long or too short?
- This is the same guarantee as a rental unit accepting one application. What differs, and what is identical?
