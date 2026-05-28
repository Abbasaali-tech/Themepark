# Theme Park Management System - Dual Portal

## 📋 Overview
The enhanced Theme Park Management System now features **two separate portals** with role-based access control:
- **Staff Portal** - For staff members to manage visitors and bookings
- **Manager Portal** - For managers to manage operations, staff, and view reports

---

## 🔐 Login Credentials

### Staff User
- **Username:** `staff1`
- **Password:** `pass123`

### Manager User
- **Username:** `manager1`
- **Password:** `admin123`

---

## 👥 Staff Portal Features

Staff members can:
1. **Register Visitor** - Add new visitors to the system
2. **View Available Rides** - Display all operational rides
3. **View Available Events** - Display all upcoming events
4. **Book Ticket for Visitor** - Create tickets for registered visitors
5. **View All Visitors** - List all registered visitors in the system

**Typical Workflow:**
- Staff logs in → Registers a visitor → Shows them rides/events → Books a ticket

---

## 🏢 Manager Portal Features

Managers can:
1. **Add Staff Member** - Hire new staff with role and salary
2. **Add Ride** - Add new attractions to the park
3. **Add Event** - Schedule new events
4. **Add Inventory Item** - Track items and supplies
5. **Update Ride** - Update ride name, fare, or status
6. **Update Event** - Update event name, date, or capacity
7. **Update Inventory** - Update item name, quantity, or cost
8. **Update Staff** - Update staff name, role, or salary
9. **Update Visitor** - Update visitor name, age, or email
10. **Update Ticket** - Update visitor, ride, or amount
11. **View Feedback** - Review visitor feedback and ratings
12. **View Revenue Report** - See total ticket revenue
13. **View All Staff** - List all employees
14. **View All Rides** - Display all rides
15. **View All Events** - Display all events
16. **View All Inventory** - Track stock levels
17. **Save Data** - Manually save all data

**Typical Workflow:**
- Manager logs in → Adds staff/rides/events → Reviews feedback → Generates revenue report

---

## 🏗️ OOP Concepts Demonstrated

### 1. **Inheritance & Polymorphism**
- `ParkEntity` abstract base class
- `Visitor`, `Ride`, `Event`, `Staff`, `Inventory` derived classes
- All use virtual `display()` and `serialize()` methods

### 2. **Encapsulation**
- Private members with public getters
- Data hiding (password not exposed)

### 3. **Abstraction**
- Abstract base class `ParkEntity` with pure virtual functions
- User authentication layer

### 4. **Operator Overloading**
- `Ticket` class: `operator+` (addition), `operator<` (comparison)
- Stream operator `<<` for output

### 5. **Static Members**
- `nextId` in each entity class for auto-incrementing IDs

### 6. **Friend Functions**
- `applyDiscount()` - modifies private Ticket members
- `calculateAverageRating()` - accesses private Feedback members

### 7. **Templates**
- `readNumber<T>()` - generic input validation
- `findById<T>()` - generic search by ID

### 8. **STL Containers**
- `vector<T>` for dynamic arrays
- `algorithm` functions: `find_if()`, `sort()`, `accumulate()`
- Lambda expressions in algorithms

### 9. **Exception Handling**
- `try-catch` blocks
- Custom `runtime_error` exceptions
- Input validation with exceptions

### 10. **File I/O**
- Serialization with pipe-delimited format
- `ifstream`/`ofstream` for persistence
- Load/save data methods

### 11. **Role-Based Access Control**
- User authentication before portal access
- Different menus for different roles
- Polymorphic behavior based on user role

### 12. **Aggregation**
- `ThemeParkSystem` contains vectors of entities
- Relationship between visitors, rides, tickets

### 13. **Constructors & Destructors**
- Parameterized constructors with default values
- Destructor for proper cleanup
- Constructor chaining

---

## 📂 Data Files Created

When you run the program, these files are automatically created:

- `Users.txt` - User login credentials
- `Visitors.txt` - Registered visitors
- `Rides.txt` - Theme park attractions
- `Tickets.txt` - Ticket bookings
- `Events.txt` - Scheduled events
- `Staff.txt` - Staff members
- `Feedback.txt` - Visitor feedback
- `Inventory.txt` - Supply inventory

---

## 🎯 Program Flow

```
Start Application
    ↓
Main Menu (Login Screen)
    ├─→ Option 1: Login as Staff
    │       ↓
    │   Enter credentials
    │       ↓
    │   Staff Portal Menu
    │   (Register visitors, book tickets, view rides/events)
    │       ↓
    │   Logout
    │
    ├─→ Option 2: Login as Manager
    │       ↓
    │   Enter credentials
    │       ↓
    │   Manager Portal Menu
    │   (Add staff/rides/events, view reports)
    │       ↓
    │   Logout
    │
    └─→ Option 0: Exit
            ↓
        Save All Data
            ↓
        End
```

---

## 🚀 Sample Usage Scenario

### Scenario 1: Staff Registration
1. Run program
2. Choose "Login as Staff" (Option 1)
3. Enter credentials: `staff1` / `pass123`
4. Choose "Register Visitor" (Option 1)
5. Enter visitor details
6. View available rides/events
7. Book ticket for visitor
8. Logout

### Scenario 2: Manager Operations
1. Run program
2. Choose "Login as Manager" (Option 2)
3. Enter credentials: `manager1` / `admin123`
4. Choose "Add Staff Member" (Option 1)
5. Enter staff details
6. Choose "View Revenue Report" (Option 12)
7. See financial analysis
8. Logout

---

## 📊 Revenue Report Breakdown

The manager's revenue report shows:
- **Total Ticket Revenue** - Income from all booked tickets

---

## 🔧 Building & Running

### Compile
```bash
g++ ThemeParkProject.cpp -std=c++17 -o ThemeParkProject.exe
```

### Run
```bash
ThemeParkProject.exe
```

---

## 💡 Key OOP Principles

| Principle | Implementation |
|-----------|-----------------|
| **Inheritance** | ParkEntity → Visitor, Ride, Event, Staff, Inventory |
| **Polymorphism** | Virtual `display()` and `serialize()` methods |
| **Encapsulation** | Private members, public interfaces |
| **Abstraction** | Abstract base classes, user authentication layer |
| **Composition** | ThemeParkSystem contains multiple entity vectors |
| **Separation of Concerns** | Staff and Manager portals isolated |

---

## ✨ Features for Viva Explanation

1. **Dual Portal Architecture** - Demonstrates understanding of role-based access
2. **Authentication System** - Shows security concepts
3. **Polymorphic Display** - All entities use same interface
4. **Financial Reporting** - Real-world application logic
5. **File Persistence** - Data survives program restarts
6. **Template Usage** - Generic functions reduce code duplication
7. **Exception Handling** - Robust error management
8. **STL Usage** - Modern C++ practices

---

## 📝 Notes

- Default users are created on first run
- All data is saved to `.txt` files in pipe-delimited format
Each entity type uses a static auto-incremented ID counter when new records are created.

