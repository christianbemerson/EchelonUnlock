# Testing Strategy

## Controlled reduction

The authentication exchange was treated as an experimental system. Instead of attempting to reverse-engineer the entire protocol at once, individual fields were changed while the rest of the interaction remained constant.

This made it possible to determine which parts of the response were meaningful and which were incidental.

## Outcome-based validation

A connection or write returning successfully was not considered proof that the bike was usable.

A successful test required:

- a stable connection,
- live cadence data,
- working resistance reporting/control where applicable,
- and repeatable behavior after reconnect or cold start.

This distinction caught cases where the authentication step appeared to succeed but the useful telemetry path was still not functioning correctly.

## Repeatability

After the reduced authentication behavior was identified, cold-start testing was repeated many times. A 20-restart test series succeeded on the first attempt each time, providing much stronger evidence than a single successful session.

## Layer isolation

A later roughly 30-second disconnect cycle was investigated separately from authentication. Candidate causes included:

- bike firmware behavior,
- BLE transport/client behavior,
- Android power management,
- and application-level virtual-device/reconnect behavior.

Treating those as separate layers prevented a working authentication solution from being incorrectly blamed for an unrelated connection-management issue.

## General lesson

For automation, "the command returned success" and "the intended state was achieved" are different assertions. Reliable systems verify the second one.
