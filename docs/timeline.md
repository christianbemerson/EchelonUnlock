# Condensed Project Timeline

## 1. Initial problem

The Echelon EX4-S hardware worked well, but third-party software could not immediately obtain a fully functional session from the bike.

## 2. Observe the official workflow

Network and BLE interactions from the official client were captured to identify where authentication occurred and how it related to telemetry availability.

## 3. Reduce the authentication exchange

The observed response was modified systematically. Controlled tests showed that only a small portion of the response was significant for the behavior being tested.

## 4. Reproduce independently

The authentication interaction was reproduced directly over BLE. This separated the bike protocol from the official application's UI and business logic.

## 5. Validate the real outcome

Some experiments demonstrated that an accepted authentication message alone was not sufficient. Success was redefined as functional live cadence and resistance data.

## 6. Reliability testing

Repeated cold-start testing was used to validate the reduced approach. A 20-restart test series succeeded first try throughout the run.

## 7. Move onto the bike tablet

The working approach was exercised from the built-in Android tablet so the bike could operate as a self-contained third-party fitness setup.

## 8. Isolate reconnect behavior

A recurring disconnect was investigated as a separate systems problem. Application/device behavior was narrowed down until the connection became stable in the intended configuration.

## 9. Upstream collaboration

Findings were shared with the QZ Fitness developer, tested across additional Echelon scenarios including iOS, and incorporated upstream.
