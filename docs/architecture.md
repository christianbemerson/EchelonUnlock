# Architecture and Data Flow

## High-level flow

```text
Bike firmware
    |
    | Bluetooth LE
    v
Client application
    |
    | authentication exchange
    v
Authenticated session
    |
    +--> cadence telemetry
    +--> resistance telemetry
    +--> control/status messages
```

The original client performs an authentication exchange before the bike exposes useful live telemetry. The research focused on identifying the minimum behavior required to establish that usable session and then validating the result at the application level.

## Components investigated

### Bluetooth LE

The bike exposes multiple BLE characteristics. Capturing notifications and writes made it possible to identify the order of operations around connection, challenge delivery, authentication, and subsequent telemetry.

### Authentication behavior

Rather than assume every byte in the observed exchange was significant, the response was reduced experimentally. Fields were modified or zeroed in controlled tests to determine which portions affected the result.

### Android client environment

After the authentication flow worked independently, the implementation was exercised on the bike's built-in Android tablet. This exposed a separate periodic disconnect problem that had to be isolated from the authentication logic itself.

### Third-party application integration

The resulting compatibility work was tested with QZ Fitness. Broader testing helped distinguish device-specific behavior from reusable Echelon-family behavior and eventually led to the support being merged upstream.

## Automation mindset

The important design principle was to define success by the end state, not by an intermediate API or BLE return value.

```text
connect
  -> authenticate
  -> verify telemetry
  -> monitor connection
  -> reconnect if needed
  -> verify telemetry again
```

That same pattern applies to operational automation: perform an action, verify the desired state, and escalate only when the automated path cannot establish that state safely.
