# Echelon EX4-S Interoperability Research

Reverse-engineering and interoperability research on an Echelon EX4-S exercise bike, focused on understanding its Bluetooth authentication flow and enabling reliable use with third-party fitness software on hardware I own.

## Why I built this

The bike exposes useful live telemetry such as cadence and resistance over Bluetooth, but the useful data path is gated behind a proprietary authentication exchange. I wanted to understand that interaction well enough to make the bike work reliably with third-party software without depending on the original application.

This became a useful systems problem rather than a single "unlock" trick. It involved Bluetooth LE, network traffic analysis, controlled experiments, Android behavior, reconnect handling, validation, and collaboration with an open-source project.

## Engineering approach

I treated the system as a black box and worked from observable inputs and outputs:

1. Captured the interaction between the official software and the bike.
2. Identified the authentication exchange that occurs before useful telemetry becomes available.
3. Reduced the response experimentally by changing one field at a time and observing the result.
4. Reproduced the authentication behavior independently over BLE.
5. Verified success using the actual outcome, live cadence and resistance, rather than assuming a successful intermediate response meant the workflow was complete.
6. Repeated cold-start and reconnect testing to distinguish a one-off success from reliable behavior.
7. Moved the working setup onto the bike's built-in Android tablet and investigated a separate recurring disconnect issue.
8. Shared the findings with the QZ Fitness project, where the compatibility work was tested more broadly and merged upstream.

## What made the project interesting

A few lessons from the project map directly to production automation work:

- **Instrument before guessing.** Capture what the system actually does, then form a hypothesis.
- **Reduce the problem.** Change one variable at a time until the minimum required behavior is understood.
- **Verify outcomes, not commands.** A successful authentication write was not enough. The bike had to expose functional cadence and resistance data.
- **Separate failures by layer.** Authentication, BLE transport, Android power behavior, and application-level reconnect logic were treated as separate problems.
- **Test repeatability.** Once the authentication behavior appeared understood, I validated it across repeated cold starts rather than relying on a single successful test.
- **Document and upstream useful work.** The end goal was not a one-off local hack, but a repeatable solution useful to other owners and maintainers.

## Result

The final workflow reliably authenticated the bike for third-party use, exposed functional cadence and resistance data, survived repeated cold starts, and was validated across additional client/device scenarios during upstream testing.

## Repository structure

- `docs/architecture.md` - high-level system and data-flow notes
- `docs/testing.md` - validation strategy and lessons learned
- `docs/timeline.md` - condensed project progression
- `scripts/README.md` - implementation notes and placeholders for sanitized tooling

## Scope and ethics

This repository documents interoperability research performed on personally owned hardware. It intentionally avoids proprietary application code, credentials, user data, and redistribution of vendor software. The goal is to document engineering methodology, compatibility work, and reproducible observations.
