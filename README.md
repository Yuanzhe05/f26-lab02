# Lab 2 Starter: Availability Calculator

A small reservation component. Given a room's bookings and the day's business hours,
`AvailabilityCalculator.freeSlots` computes when the room is free. It is the code you
work in for Lab 2.

It ships with a generated test suite that passes, and a property-based test harness
(jqwik) with one example property. Everything is green. Your job in Lab 2 is to decide
whether green actually means correct.

**Read `ARCHITECTURE.md` before the code.**

## Agent used
Codex with 5.6 Sol, medium.

## M2
The calculator omitted the final free interval after the last booking.

## M3
- **Controllability gap:** None of the exact-result tests had free time left after
  the last booking. The last booking always went to closing time, so the bug did
  not show up in those tests.
- **Controllability gap:** There was no test with an empty booking list. That case
  should return the whole day as free, but the buggy code returned nothing.
- **Observability gap:** The overlap test did use a booking that ended early, but it
  only looked at the slots that were returned. It did not check whether any free
  time was missing.

The line coverage was high because the tests ran most of the code that was there.
It could not tell us that the code for adding the last free slot was missing.

## Build and test

```
mvn test
```

`mvn test` runs both files, the ordinary example-based tests (`AvailabilityCalculatorTest`)
and the property-based tests (`AvailabilityProperties`). A code-coverage report is written
to `target/site/jacoco/index.html`.

## Continuous integration

This repository has CI configured in `.github/workflows/ci.yml`. GitHub disables workflows on a
fresh fork, so enable them once on your fork (the handout shows where). After that, every
push runs `mvn test`. You will watch the gate go red when your new property finds the bug, then
green once you fix it.

## Where things are

- Component: `src/main/java/edu/cmu/cs214/availability/`
- Example-based tests: `src/test/java/edu/cmu/cs214/availability/AvailabilityCalculatorTest.java`
- Property-based tests: `src/test/java/edu/cmu/cs214/availability/AvailabilityProperties.java`
- Setup: `SETUP.md`

See the Lab 2 handout on the course page for the three milestones you show a TA.
