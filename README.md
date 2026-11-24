# Amusement Park Ticketing and Ride Access System

A console-based Java application for selling tickets, managing visitor wallets,
validating ride access, tracking queues, and generating reports.

Requires Java 8 or newer.

## Build and run

From this folder:

```
javac -d out $(find src -name "*.java")
java -cp out ui.Main
```

On Windows (Command Prompt):

```
dir /s /b src\*.java > sources.txt
javac -d out @sources.txt
java -cp out ui.Main
```

Data is saved to `parkdata.ser` in the folder you run from, and loaded on the next start.
Delete that file to reset everything.

## Project structure

```
src/
  model/      Scanable, Attraction, Ride, RideStatus, Ticket, StandardTicket,
              VIPTicket, SeasonPass, Visitor, Transaction, TurnstileEntry
  service/    ParkSystem (business rules), ReportService, DataStore
  ui/         Main (menu and input validation)
```

## OOP mapping

| Pillar        | Where                                                                                   |
|---------------|-----------------------------------------------------------------------------------------|
| Abstraction   | `abstract Ticket`, `abstract Attraction`, `interface Scanable`                          |
| Encapsulation | Private fields + validated setters in `Visitor`, `Ride`; read-only `Transaction`        |
| Inheritance   | `StandardTicket`, `VIPTicket`, `SeasonPass` extend `Ticket`; `Ride` extends `Attraction` |
| Polymorphism  | `calculatePrice()`, `validateAccess()`, `isValidOn()`, `hasPriorityAccess()` overridden per ticket type; `Ride.setStatus()` overridden |

## Quick demo flow

1. Ticket menu -> register a visitor (gets ID `V-001`)
2. Wallet menu -> top up `V-001`
3. Ticket menu -> buy a ticket (gets ID `T-0001`)
4. Ride Access menu -> scan the ticket at the turnstile, then check access for a ride
5. Queue menu -> join a queue, release visitors, change ride status
6. Reports menu -> daily sales, entry log, ride usage
