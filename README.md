# Amusement-Park-Ticketing-and-Ride-Access-System
**Description:** Development of a Java-based Amusement Park Ticketing and Ride Access System for Managing Ticket Sales, Visitor Wallets, Ride Restrictions, and Queue Monitoring

## Project Description
Many amusement parks still handle ticketing and ride access manually. Visitors line up at cash counters where staff count money, issue paper tickets, and write down sales by hand. During weekends and holidays these queues grow long, visitors lose ride time, and staff are overloaded with repetitive cash handling.

Ride restrictions are also checked by eye. Operators estimate a visitor's height, ask about their age, and inspect a ticket to confirm VIP or season-pass privileges. This is slow, inconsistent, and dependent on the operator's judgment, and no record is kept of who rode what.

The proposed system automates ticket sales, cashless visitor wallets, ride eligibility checks, queue monitoring, and reporting in one consistent and auditable application.

## Problem being addressed
The project addresses the bottlenecks created by manual ticketing and ride access control in amusement parks.

Cash-handling queues slow down visitors and staff. Miscounted change, unrecorded sales, duplicated tickets, and missing entry logs make it hard to reconcile daily income against actual attendance, which causes revenue leaks. Height, age, and ticket-type checks done by hand are inconsistent, and the lack of records makes safety incidents difficult to trace.

The system addresses these problems by providing a digital platform for selling tickets, validating ride access automatically, tracking queues, and generating reports.

## Project Objectives
### General Objective:
To develop a Java-based Amusement Park Ticketing and Ride Access System for managing ticket sales, visitor wallets, ride restrictions, and queue monitoring.

#### Specific Objectives:

1. Identify common problems in manual ticketing, cash handling, and ride restriction checking.

2. Determine the necessary features and functionalities of the system.

3. Design and develop a digital system for ticket purchasing, wallet management, ride access validation, queue tracking, and reporting.

4. Apply the four pillars of Object-Oriented Programming (abstraction, encapsulation, inheritance, and polymorphism) in the design of the system.

5. Evaluate the system in terms of functionality, usability, reliability, and efficiency.

## Target Users
### Park Staff (Ticket Counter and Ride Operators)
- **Register visitors and sell Standard, VIP, or Season tickets.**

- **Top up visitor wallets and check balances.**

- **Scan tickets at the entrance and check ride access.**

- **Manage ride queues and open or close rides.**

### Park Management
- **Review daily sales revenue by ticket type.**

- **Review turnstile entry logs.**

- **Monitor ride usage and live ride status.**

### Visitors
- **Receive faster service through cashless wallets and instant ticketing.**

- **Get clear, consistent reasons when ride access is granted or denied.**

## Main Features

| Feature | Description |
|---|---|
| Ticket Purchasing & Management | Sells Standard, VIP, or Season tickets to a registered visitor, issues a unique ticket ID, records the transaction, and supports viewing or cancelling tickets with a wallet refund. |
| Digital Wallet & Top-up | Gives each visitor a cashless wallet. Supports adding funds, checking the balance, and deducting ticket payments. Rejects purchases with insufficient balance. |
| Ride Access & Restriction Validator | Checks a visitor's height, age, and ticket type against a ride's requirements and returns Access Granted or Denied with a specific reason. Also scans tickets at the park entrance turnstile. |
| Queue & Capacity Tracking | Shows each ride's live status (open, closed, maintenance), queue count, and capacity. Staff can add or release visitors and change ride status. |
| Reporting & Statistics | Generates daily sales revenue by ticket type, the turnstile entry log, and ride usage counts. |
| Input Validation | Rejects empty, non-numeric, or out-of-range input and re-prompts the user instead of crashing. |
| Data Saving | Saves all visitors, tickets, transactions, and logs when the program exits and loads them on the next start. |

## Application Workflow

```
Start
↓
Main Menu
↓
Select Operation
↓
Enter Information
↓
Validate Input
↓
Process Request
↓
Display Result
↓
Return to Main Menu
↓
Exit
```

## Technologies Used

The Amusement Park Ticketing and Ride Access System uses the following technologies:

- **Java Programming Language** – Used to develop the system and implement its functionalities.
- **Object-Oriented Programming (OOP)** – Used to organize the program through classes, objects, methods, and OOP principles.
- **Java Serialization** – Used to save and load the system's data in a file (`parkdata.ser`).
- **GitHub** – Used as the source code repository and for project collaboration.

## Project Structure

```
src/
  model/      Scanable, Attraction, Ride, RideStatus, Ticket, StandardTicket,
              VIPTicket, SeasonPass, Visitor, Transaction, TurnstileEntry
  service/    ParkSystem (business rules), ReportService, DataStore
  ui/         Main (menus and input validation)
run.bat       Compiles and starts the program on Windows
```

| Package | Responsibility |
|---|---|
| `model` | The data and rules of each object: tickets, rides, visitors, and transactions. |
| `service` | The business logic (`ParkSystem`), report building (`ReportService`), and saving or loading data (`DataStore`). |
| `ui` | The console menus and input checking (`Main`). |

## Team Members and Roles

| Team Member | Role and Responsibilities |
|---|---|
| [Member 1 name] | Project Leader – Coordinates team activities and monitors project completion. |
| [Member 2 name] | Develops the ticket classes (`Ticket`, `StandardTicket`, `VIPTicket`, `SeasonPass`). |
| [Member 3 name] | Develops the `ParkSystem` class and the purchase, wallet, queue, and access functionalities. |
| [Member 4 name] | Develops the main menu, user input, and program flow; helps integrate the classes. |
| [Member 5 name] | Tests and debugs the system; prepares documentation, screenshots, and presentation. |

## OOP Concepts Demonstrated

The Amusement Park Ticketing and Ride Access System demonstrates the fundamental Object-Oriented Programming (OOP) concepts through its classes, objects, attributes, and methods.

#### 1. Abstraction

Abstraction is implemented through the abstract classes `Ticket` and `Attraction` and the interface `Scanable`. They define what every ticket or attraction must be able to do, while the subclasses decide how.

```java
public abstract class Ticket implements Scanable, Serializable {
    public abstract double calculatePrice();
    public abstract boolean validateAccess(Ride ride);
    public abstract boolean isValidOn(LocalDate date);
}

public interface Scanable {
    boolean scan();
    String getScanCode();
}
```

#### 2. Encapsulation

Encapsulation is implemented by keeping the attributes of `Visitor`, `Ride`, and `Transaction` private and accessing or changing them only through public methods that validate the data. `Transaction` has no setters, so a recorded transaction cannot be altered.

```java
public class Visitor {
    private String name;
    private double walletBalance;

    public void setName(String name) {
        if (name == null || name.trim().isEmpty()) {
            throw new IllegalArgumentException("Visitor name cannot be empty.");
        }
        this.name = name.trim();
    }

    public boolean deductFunds(double amount) {
        if (amount > walletBalance) {
            return false;
        }
        walletBalance -= amount;
        return true;
    }
}
```

#### 3. Inheritance

Inheritance is demonstrated through `StandardTicket`, `VIPTicket`, and `SeasonPass`, which extend the parent `Ticket` class, and through `Ride`, which extends `Attraction`. They inherit the common fields and methods and add their own rules.

```java
public class StandardTicket extends Ticket { }

public class VIPTicket extends Ticket { }

public class SeasonPass extends Ticket { }

public class Ride extends Attraction { }
```

#### 4. Polymorphism

Polymorphism allows different ticket types to use the same method name but provide different behavior. `calculatePrice()` and `validateAccess()` are overridden in each ticket class, so the program can call them on any `Ticket` and the correct version runs.

```java
public class StandardTicket extends Ticket {
    @Override
    public double calculatePrice() {
        return PRICE;
    }
}

public class VIPTicket extends Ticket {
    @Override
    public double calculatePrice() {
        return StandardTicket.PRICE + VIP_PREMIUM;
    }

    @Override
    public boolean hasPriorityAccess() {
        return true;
    }
}

Ticket ticket = new VIPTicket(id, visitor, today);
double price = ticket.calculatePrice();   // runs VIPTicket's version
```

#### 5. Classes and Objects

The system uses classes as blueprints for creating objects. Each visitor, ticket, ride, and transaction is an object containing its own information.

```java
Visitor visitor = new Visitor("V-001", "Alice", 25, 165);
Ticket ticket = new StandardTicket("T-0001", visitor, LocalDate.now());
Ride ride = new Ride("Roller Coaster", 130, 200, 10, 24, false);
```

#### 6. Methods

Methods perform the different operations of the system, including registering visitors, buying tickets, topping up wallets, validating access, and managing queues.

```java
park.registerVisitor(name, age, height);
park.purchaseTicket(visitorId, ticketType);
park.topUp(visitorId, amount);
park.joinQueue(ticketId, rideNumber);
```

#### 7. Exception Handling

Exception handling prevents the program from terminating unexpectedly when users enter invalid information. The service layer throws descriptive exceptions, and the menu catches them and shows a readable error message.

```java
try {
    park.purchaseTicket(visitorId, type);
} catch (IllegalArgumentException | IllegalStateException e) {
    System.out.println("Error: " + e.getMessage());
}
```

#### 8. Collections and Data Handling

The system uses collections such as `LinkedHashMap` and `ArrayList` to store visitors, tickets, transactions, rides, and the turnstile log. This allows the application to look up, display, update, and report on the data.

```java
private final Map<String, Visitor> visitors = new LinkedHashMap<>();
private final Map<String, Ticket> tickets = new LinkedHashMap<>();
private final List<Transaction> transactions = new ArrayList<>();
```

## Instructions for Running

### Requirements
- Java Development Kit (JDK) 8 or newer installed
- Java compiler (`javac`) available in the system PATH
- Windows operating system (to use `run.bat`)

### Steps
1. Download or clone this repository.
2. Open the project folder (the folder that contains `src` and `run.bat`).
3. Double-click `run.bat`, or run it from Command Prompt.
4. The batch file will compile the Java source files and launch the application.
5. If compilation fails, check that the JDK is installed and that the source files are correctly organized (`src\model`, `src\service`, and `src\ui`).

### Running manually
From the project folder:

```
javac -d out src\model\*.java src\service\*.java src\ui\*.java
java -cp out ui.Main
```

Data is saved to `parkdata.ser` in the folder you run the program from. Delete that file to reset all visitors, tickets, and sales.

### Quick demo flow
1. Ticket menu → register a visitor (gets ID `V-001`).
2. Wallet menu → top up `V-001`.
3. Ticket menu → buy a ticket (gets ID `T-0001`).
4. Ride Access menu → scan the ticket at the turnstile, then check access for a ride.
5. Queue menu → join a queue, release visitors, change ride status.
6. Reports menu → daily sales, entry log, ride usage.

## Sample Screenshots

The following screenshots show the interface and main functionalities of the Amusement Park Ticketing and Ride Access System. Add your own screenshots to a `Screenshots` folder using these file names.

#### 1. Main Interface

This screenshot shows the main menu, where users can access the available operations.

![Main Interface](Screenshots/Main%20Menu.png)

#### 2. Ticket Purchase

This feature allows staff to register a visitor and buy a Standard, VIP, or Season ticket.

![Ticket Purchase](Screenshots/Ticket%20Purchase.png)

#### 3. Wallet Top-up

This screenshot shows adding funds to a visitor's wallet and checking the balance.

![Wallet Top-up](Screenshots/Wallet%20Top-up.png)

#### 4. Ride Access Validation

This screenshot shows an Access Granted or Access Denied result with the reason, based on height, age, and ticket type.

![Ride Access Validation](Screenshots/Ride%20Access.png)

#### 5. Queue and Capacity Tracking

This screenshot shows the live ride board with each ride's status, queue count, and capacity.

![Queue Tracking](Screenshots/Queue%20Tracking.png)

#### 6. Reports

This screenshot shows the daily sales revenue report and the turnstile entry log.

![Reports](Screenshots/Reports.png)

## Known Limitations

The Amusement Park Ticketing and Ride Access System has the following limitations:

#### 1. Console-Based Application
The system only runs as a Java console-based application and does not include a graphical user interface (GUI).

#### 2. No User Registration or Login
The system does not support staff or visitor accounts, so anyone who can run the program can use every function.

#### 3. No Real Payment Processing
Wallet top-ups are recorded by staff and are not connected to a real payment system. Money is stored as `double` values for simplicity.

#### 4. Local File Storage Only
Data is saved to a single local file (`parkdata.ser`) and is not shared between computers or backed up online.

#### 5. Simplified Queues and Ticket Rules
Queues are counters rather than lists of individual visitors, ride restrictions are fixed in the code, and Standard and VIP tickets are valid only on the day of purchase.

## Future Improvements

The following improvements may be considered for future development to enhance the functionality and usability of the system.

#### 1. Graphical User Interface (GUI)
Develop a user-friendly graphical interface to make the application easier to navigate and use.

#### 2. Staff Login and Roles
Add accounts and permissions so that ticket staff, ride operators, and management only see the functions they need.

#### 3. QR Code or Barcode Tickets
Generate scannable codes for tickets so that turnstiles and ride gates can read them automatically.

#### 4. Database and Online Storage
Store data in a database so that several counters and ride gates can share the same live information.

#### 5. Online Booking and Payment
Allow visitors to buy tickets and top up wallets online before arriving at the park.

## Project Contributors

The Amusement Park Ticketing and Ride Access System was developed by [Team name], from Section [Section] as part of the [Course name and code] course.

#### Team Members and Roles

1. **[Member 1 name]** – Project Leader; coordinates tasks and checks project completion.

2. **[Member 2 name]** – Develops the ticket classes.

3. **[Member 3 name]** – Develops the `ParkSystem` class and its functionalities.

4. **[Member 4 name]** – Develops the main menu, user input, and program flow; assists with class integration.

5. **[Member 5 name]** – Handles system testing and debugging, documentation, screenshots, and presentation.

#### Acknowledgment

We would like to acknowledge the contributions and efforts of every team member in planning, developing, testing, and documenting the Amusement Park Ticketing and Ride Access System.
