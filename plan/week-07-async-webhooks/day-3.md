# Week 7, Day 3: Domain events on the Bill aggregate

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Learn events and listeners in Laravel.** An event is a message. A listener is a class that reacts to it. Laravel wires the two through an event dispatcher.
   - Laravel events: https://laravel.com/docs/events

2. **Have the Bill aggregate raise `PaymentReceived` and `BillSettled` as domain events.** Not framework events for their own sake — these are events *of the domain*. The Bill produces them because something meaningful happened *to the Bill*: money came in, or the target was covered. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

3. **Understand the difference between a Laravel event and a DDD domain event.** A Laravel event is a technical message on a dispatcher. A DDD domain event is a first-class domain concept named in the ubiquitous language — "PaymentReceived", not "BillUpdated". It happens to be dispatched by Laravel's event system, but its meaning is domain, not infrastructure. Be able to say this out loud.

4. **Attach listeners.** A `SendPaymentConfirmation` listener on `PaymentReceived`. A `NotifyAllPayers` listener on `BillSettled`. Each listener implements `ShouldQueue` so it runs on a worker, not inline.

5. **Raise events inside the same transaction as the state change.** Or, more precisely, record them on the aggregate during the transaction and dispatch them after commit. Dispatching before commit risks a listener acting on state that then rolls back.

## Cross-cutting reminders

- **Tactical DDD**: `PaymentReceived` and `BillSettled` are domain events raised by the aggregate — named in the ubiquitous language, not framework-flavoured. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: every state change the aggregate raises still writes an audit entry inside the same transaction as the change. Domain events are for reacting; the audit log is for the record. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None.
