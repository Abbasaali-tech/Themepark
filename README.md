# Theme Park Management System (C++)

Theme Park Management System is a C++ console application developed for the Object Oriented Programming (OOP) Lab. It models daily park operations such as visitor registration, ride management, event scheduling, ticket booking, staff management, feedback collection, inventory control, and revenue tracking. The system uses a menu-driven interface with role-based access for staff and manager, and persists all data using file handling.

## Highlights

- Role-based login for staff and manager.
- Menu-driven console interface for all operations.
- Persistent storage using text files (pipe-separated values).
- Core entities modeled with inheritance, encapsulation, and polymorphism.
- Ticket booking with discount support and revenue reporting.
- Update features for rides, events, inventory, staff, visitors, and tickets.

## Features

### Staff Portal

- Register visitors.
- View available rides and events.
- Book tickets for visitors.
- View all visitors.

### Manager Portal

- Add staff, rides, events, and inventory.
- Update rides (name, fare, status).
- Update events (name, date, capacity).
- Update inventory (name, quantity, cost).
- Update staff (name, role, salary).
- Update visitors (name, age, email).
- Update tickets (visitor, ride, amount).
- View feedback and average rating.
- View revenue report.
- Save all data.

## OOP Concepts Implemented

- Classes and objects for all entities.
- Encapsulation with private data and getters/setters.
- Inheritance using `ParkEntity` as base class.
- Polymorphism via virtual `display()` and `serialize()`.
- Abstraction through the abstract base class.
- Operator overloading for ticket operations and output.
- Templates for input handling and ID lookup.
- Exception handling for invalid input and missing records.
- Static members for auto-incrementing IDs.

## File Storage Format

Data is stored in text files in the project directory. Each record uses the pipe separator (`|`).

- Visitors.txt: id|name|age|email
- Rides.txt: id|name|price|operational
- Tickets.txt: id|visitorId|rideId|amount
- Events.txt: id|name|date|capacity|registered
- Staff.txt: id|name|role|salary
- Feedback.txt: id|visitorId|rating|comment
- Inventory.txt: id|name|quantity|costPerItem
- Users.txt: userId|username|password|role

## Default Credentials

If no users exist, the system seeds default accounts:

- Staff: username `staff1`, password `pass123`
- Manager: username `manager1`, password `admin123`

## Build and Run (Windows)

Compile:

```
g++ ThemeParkProject.cpp -o ThemeParkProject.exe
```

Run:

```
ThemeParkProject.exe
```

## Project Files

- ThemeParkProject.cpp: Main application source.
- ThemeParkProject.exe: Compiled executable (if present).
- themepark_proposal.html / themepark_report.html: Project documents.
- *.txt: Data storage files.
- *.png: Screenshots of menus and reports.

## Screenshots

| Screen | Preview |
| --- | --- |
| Main Menu | ![Main Menu](/images/main_menu.png) |
| Staff Portal | ![Staff Portal](/images/staff_portal.png) |
| Manager Portal | ![Manager Portal](/images/manager_portal.png) |
| Revenue Report | ![Revenue Report](/images/revenue_report.png) |

## Notes

- All data changes are saved to text files and reloaded on startup.
- Tickets use ride price at time of booking; updates can modify ticket amount manually.
- Event capacity cannot be set below registered count.
