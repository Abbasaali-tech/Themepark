# Theme Park Management System - Complete Documentation

## 📋 Table of Contents

1. [System Overview](#system-overview)
2. [Getting Started](#getting-started)
3. [Class Architecture & Relationships](#class-architecture--relationships)
4. [User Roles & Portal System](#user-roles--portal-system)
5. [Staff Portal - Complete Guide](#staff-portal--complete-guide)
6. [Manager Portal - Complete Guide](#manager-portal--complete-guide)
7. [Program Flow & Architecture](#program-flow--architecture)
8. [Data Structure & File Format](#data-structure--file-format)
9. [Sample Data](#sample-data)
10. [OOP Concepts Implementation](#oop-concepts-implementation)

---

## System Overview

### What is This System?

The **Theme Park Management System** is a comprehensive C++ application designed to manage all operations of a theme park. It provides two distinct portals (Staff Portal and Manager Portal) that allow different users to perform different tasks related to visitors, rides, events, inventory, and financial reports.

### Key Features

✅ **Dual Portal System** - Separate interfaces for Staff and Manager  
✅ **User Authentication** - Login system with username and password  
✅ **Visitor Management** - Register and track park visitors  
✅ **Ride Management** - Manage rides with operational status  
✅ **Event Management** - Schedule and track events (Eid Festival, Bake Sale, etc.)  
✅ **Ticket Booking** - Book tickets for visitors with discount support  
✅ **Staff Management** - Add and manage park staff  
✅ **Inventory Management** - Track items like food and merchandise  
✅ **Feedback System** - Collect and analyze visitor feedback with ratings  
✅ **Revenue Reports** - Generate financial reports for managers  
✅ **Data Persistence** - Save and load all data from files  

---

## Getting Started

### How to Run

1. **Navigate to the project folder**
  ```bash
  cd <project-folder>
  ```

2. **Run the executable**
   ```bash
   ThemeParkProject.exe
   ```

3. **Or compile from source**
   ```bash
   g++ ThemeParkProject.cpp -std=c++17 -o ThemeParkProject.exe
   ```

### Login Credentials

| Role | Username | Password | Description |
|------|----------|----------|-------------|
| **Staff** | `staff1` | `pass123` | Registers visitors, books tickets, views information |
| **Manager** | `manager1` | `admin123` | Adds rides, events, staff; generates reports |

---

## Class Architecture & Relationships

### System Architecture Diagram

```
ThemeParkSystem (Main System Class)
│
├── User (Authentication Class)
│   └── Role-based access and credential checks
│
├── ParkEntity (Abstract Base Class)
│   ├── Visitor (Derived)
│   ├── Ride (Derived)
│   ├── Event (Derived)
│   ├── Staff (Derived)
│   └── Inventory (Derived)
│
├── Ticket (Standalone Class with Operator Overloading)
│   └── Uses Friend Functions
│
├── Feedback (Standalone Class with Aggregation)
│   └── Uses Friend Function for average calculation
│
└── ConsoleColor (Utility Class for UI)
    └── Color management for terminal output
```

---

## Detailed Class Descriptions

### 1. **ConsoleColor** (Utility Class)

**Purpose:** Manage colored text output in the console

**Attributes:**
- `enum Color`: CYAN (3), GREEN (2), RED (4), WHITE (7), BLACK (0)

**Methods:**
- `setColor(Color foreground)` - Sets text color
- `reset()` - Resets to white
- `printTitle(const string &text)` - Prints in CYAN
- `printSuccess(const string &text)` - Prints in GREEN with checkmark
- `printError(const string &text)` - Prints in RED

**Where Used:** All menu displays and success/error messages

---

### 2. **ParkEntity** (Abstract Base Class)

**Purpose:** Base class for all park entities (Visitor, Ride, Event, Staff, Inventory)

**Access Level:** `protected`

**Attributes:**
- `int id` - Unique identifier
- `string name` - Entity name

**Methods:**
- `int getId() const` - Get entity ID
- `string getName() const` - Get entity name
- `virtual void display() const = 0` - **Pure virtual** (must be overridden)
- `virtual string serialize() const = 0` - **Pure virtual** (must be overridden)

**OOP Concepts:**
- **Abstraction** - Cannot be instantiated directly
- **Polymorphism** - Derived classes override display() and serialize()
- **Inheritance** - 5 classes derive from this

---

### 3. **Visitor** (Derived from ParkEntity)

**Purpose:** Represents a visitor in the park

**Attributes:**
- `int age` - Visitor's age (1-120)
- `string email` - Email address
- `static int nextId` - **Static member** for auto-incrementing IDs (starts at 1)

**ID Range:** 1-999

**Methods:**
- `Visitor(const string &name, int age, const string &email)` - Constructor with auto ID
- `Visitor(int id, const string &name, int age, const string &email)` - Constructor with specified ID
- `int getAge() const` - Get age
- `string getEmail() const` - Get email
- `void display() const override` - Prints visitor details
- `string serialize() const override` - Converts to file format: `ID|Name|Age|Email`

**File Format Example:**
```
1|Abbas|28|abbas@email.com
2|Taher|25|taher@email.com
```

---

### 4. **Ride** (Derived from ParkEntity)

**Purpose:** Represents a ride in the theme park

**Attributes:**
- `double price` - Cost to ride (0.00 - 10000.00)
- `bool operational` - Whether ride is open (true) or in maintenance (false)
- `static int nextId` - **Static member** for auto-incrementing IDs (starts at 1)

**ID Range:** 1-999

**Methods:**
- `Ride(const string &name, double price, bool operational)` - Constructor with auto ID
- `Ride(int id, const string &name, double price, bool operational)` - Constructor with specified ID
- `double getPrice() const` - Get ride price
- `bool isOperational() const` - Check if operational
- `void display() const override` - Prints ride details with status
- `string serialize() const override` - Converts to file format: `ID|Name|Price|Operational(1/0)`

**File Format Example:**
```
1|Roller Coaster|150.00|1
2|Ferris Wheel|100.00|1
3|Bumper Cars|75.00|1
```

---

### 5. **Event** (Derived from ParkEntity)

**Purpose:** Represents special events in the park

**Attributes:**
- `string date` - Event date (format: YYYY-MM-DD)
- `int capacity` - Maximum number of registered visitors
- `int registered` - Current number of registered visitors
- `static int nextId` - **Static member** for auto-incrementing IDs (starts at 2001)

**ID Range:** 2001-2999

**Methods:**
- `Event(const string &name, const string &date, int capacity)` - Constructor with auto ID
- `Event(int id, const string &name, const string &date, int capacity, int registered)` - With specified ID
- `string getDate() const` - Get event date
- `int getCapacity() const` - Get max capacity
- `int getRegistered() const` - Get current registrations
- `void registerVisitor()` - Register visitor for event (throws exception if full)
- `void display() const override` - Prints event details with registration status
- `string serialize() const override` - Converts to file format: `ID|Name|Date|Capacity|Registered`

**File Format Example:**
```
2001|Eid Festival|2026-04-29|500|150
2002|Bake Sale|2026-05-03|200|50
2003|Chand Raat|2026-05-01|300|80
```

---

### 6. **Staff** (Derived from ParkEntity)

**Purpose:** Represents park staff members

**Attributes:**
- `string role` - Job role (Manager, Operator, Guide, etc.)
- `double salary` - Monthly salary (0.00 - 100000.00)
- `static int nextId` - **Static member** for auto-incrementing IDs (starts at 3001)

**ID Range:** 3001-3999

**Methods:**
- `Staff(const string &name, const string &role, double salary)` - Constructor with auto ID
- `Staff(int id, const string &name, const string &role, double salary)` - With specified ID
- `string getRole() const` - Get role
- `double getSalary() const` - Get salary
- `void display() const override` - Prints staff details
- `string serialize() const override` - Converts to file format: `ID|Name|Role|Salary`

**File Format Example:**
```
3001|Hassan Ali|Manager|45000.00
3002|Amina Khan|Operator|25000.00
3003|Omar Sheikh|Guide|20000.00
```

---

### 7. **Inventory** (Derived from ParkEntity)

**Purpose:** Track items and supplies in the park

**Attributes:**
- `int quantity` - Current quantity of item (0 - 100000)
- `double costPerItem` - Cost per unit (0.00 - 1000.00)
- `static int nextId` - **Static member** for auto-incrementing IDs (starts at 4001)

**ID Range:** 4001-4999

**Methods:**
- `Inventory(const string &itemName, int quantity, double costPerItem)` - Constructor with auto ID
- `Inventory(int id, const string &itemName, int quantity, double costPerItem)` - With specified ID
- `int getQuantity() const` - Get quantity
- `double getCostPerItem() const` - Get unit cost
- `void updateQuantity(int change)` - Add/subtract quantity (throws if insufficient)
- `void display() const override` - Prints inventory details
- `string serialize() const override` - Converts to file format: `ID|ItemName|Quantity|CostPerItem`

**File Format Example:**
```
4001|Popcorn|150|2.50
4002|Ice Cream|200|1.50
4003|Soft Drinks|300|1.75
```

---

### 8. **Ticket** (Standalone Class)

**Purpose:** Represents a ticket for a ride purchase

**Attributes:**
- `int id` - Unique ticket ID
- `int visitorId` - ID of visitor who bought ticket
- `int rideId` - ID of ride ticket is for
- `double amount` - Price of ticket (after any discounts)
- `static int nextId` - **Static member** for auto-incrementing IDs (starts at 1001)

**ID Range:** 1001-9999

**OOP Concepts:**
- **Operator Overloading** (2 operators):
  - `double operator+(const Ticket &other)` - Add two ticket amounts
  - `bool operator<(const Ticket &other)` - Compare ticket amounts
- **Friend Function** (1 function):
  - `friend void applyDiscount(Ticket &ticket, double percentage)` - Modify ticket amount
- **Friend Stream Operator**:
  - `friend ostream &operator<<(ostream &os, const Ticket &ticket)` - Print ticket

**Methods:**
- `Ticket(int visitorId, int rideId, double amount)` - Constructor with auto ID
- `Ticket(int id, int visitorId, int rideId, double amount)` - With specified ID
- `int getId() const` - Get ticket ID
- `int getVisitorId() const` - Get visitor ID
- `int getRideId() const` - Get ride ID
- `double getAmount() const` - Get ticket price
- `string serialize() const` - Converts to file format: `ID|VisitorID|RideID|Amount`

**File Format Example:**
```
1001|1|1|150.00
1002|2|2|90.00
1003|3|3|75.00
```

---

### 9. **Feedback** (Standalone Class with Aggregation)

**Purpose:** Collect and store visitor feedback

**Attributes:**
- `int id` - Unique feedback ID
- `int visitorId` - ID of visitor giving feedback
- `int rating` - Rating out of 5 (1-5)
- `string comment` - Visitor's comment
- `static int nextId` - **Static member** for auto-incrementing IDs (starts at 5001)

**ID Range:** 5001-5999

**OOP Concepts:**
- **Aggregation** - Contains visitor data but doesn't own it
- **Friend Function** - `friend double calculateAverageRating(const vector<Feedback> &feedbacks)`

**Methods:**
- `Feedback(int visitorId, int rating, const string &comment)` - Constructor with auto ID
- `Feedback(int id, int visitorId, int rating, const string &comment)` - With specified ID
- `int getId() const` - Get feedback ID
- `int getVisitorId() const` - Get visitor ID
- `int getRating() const` - Get rating (1-5)
- `string getComment() const` - Get comment
- `void display() const` - Prints feedback details
- `string serialize() const` - Converts to file format: `ID|VisitorID|Rating|Comment`

**File Format Example:**
```
5001|1|5|Amazing experience! Worth every penny
5002|2|4|Great rides, but lines were long
5003|3|5|Perfect event, loved the atmosphere
```

---

### 10. **User** (Authentication Class)

**Purpose:** Represent system users with roles

**Attributes:**
- `int userId` - Unique user ID
- `string username` - Login username
- `string password` - Login password
- `string role` - Role ("Staff" or "Manager")

**Methods:**
- `User(int userId, const string &username, const string &password, const string &role)` - Constructor
- `int getUserId() const` - Get user ID
- `string getUsername() const` - Get username
- `string getRole() const` - Get role
- `bool authenticate(const string &pwd) const` - Check password
- `string serialize() const` - Converts to file format: `UserID|Username|Password|Role`

**Default Users:**
```
1001|staff1|pass123|Staff
2001|manager1|admin123|Manager
```

---

### 11. **ThemeParkSystem** (Main System Class)

**Purpose:** Orchestrate the entire theme park management system

**Data Members (STL Containers):**
- `vector<Visitor> visitors` - All visitors
- `vector<Ride> rides` - All rides
- `vector<Ticket> tickets` - All tickets sold
- `vector<Event> events` - All events
- `vector<Staff> staff` - All staff members
- `vector<Feedback> feedbacks` - All feedback
- `vector<Inventory> inventory` - All inventory items
- `vector<User> users` - All system users
- `User *currentUser` - Pointer to logged-in user

**File Mappings:**
| Class | File |
|-------|------|
| Visitors | Visitors.txt |
| Rides | Rides.txt |
| Tickets | Tickets.txt |
| Events | Events.txt |
| Staff | Staff.txt |
| Feedback | Feedback.txt |
| Inventory | Inventory.txt |
| Users | Users.txt |

**Key Methods:**
- `void run()` - Main program loop
- `bool login(const string &role)` - Authenticate user
- `void staffPortal()` - Staff interface
- `void managerPortal()` - Manager interface
- `void saveData()` - Save all data to files
- `void loadData()` - Load all data from files

---

## User Roles & Portal System

### Two-Portal Architecture

The system has **TWO completely separate portals** based on user role:

```
Main Menu (Choose Role)
    ↓
    ├─→ STAFF PORTAL (staff1/pass123)
    │    └─→ Limited Functions (Register visitors, view info, book tickets)
    │
    └─→ MANAGER PORTAL (manager1/admin123)
         └─→ Full Functions (Add everything, view reports)
```

---

## Staff Portal - Complete Guide

### Access Requirements
- **Username:** `staff1`
- **Password:** `pass123`
- **Role:** Staff

### Staff Portal Menu

```
=== Staff Menu ===
1. Register Visitor
2. View Available Rides
3. View Available Events
4. Book Ticket for Visitor
5. View All Visitors
6. Logout
```

### What Staff Can Do - Detailed

#### **1. Register Visitor**

**Purpose:** Add new visitors to the park

**Steps:**
1. Select option "1" from Staff Menu
2. Enter visitor name
3. Enter visitor age (1-120)
4. Enter visitor email
5. System auto-generates Visitor ID (starts at 1)

**Example:**
```
Enter visitor name: Abbas
Enter age: 28
Enter email: abbas@email.com

✓ Visitor added.

New Visitor ID: 1
```

**Data Storage:** Saved to `Visitors.txt`

**Format:** `VisitorID|Name|Age|Email`

---

#### **2. View Available Rides**

**Purpose:** See all rides and their status

**Steps:**
1. Select option "2" from Staff Menu
2. System displays all rides with:
   - Ride ID
   - Ride Name
   - Price
   - Status (Operational or Maintenance)

**Example Output:**
```
--- Rides ---
Ride ID: 1 | Name: Roller Coaster | Price: $150.00 | Status: Operational
Ride ID: 2 | Name: Ferris Wheel | Price: $100.00 | Status: Operational
Ride ID: 3 | Name: Bumper Cars | Price: $75.00 | Status: Operational
Ride ID: 4 | Name: Log Flume | Price: $120.00 | Status: Operational
Ride ID: 5 | Name: Teacup Ride | Price: $50.00 | Status: Operational
```

**Use Case:** Staff needs to know which rides are available for booking

---

#### **3. View Available Events**

**Purpose:** See all upcoming events

**Steps:**
1. Select option "3" from Staff Menu
2. System displays all events with:
   - Event ID
   - Event Name
   - Date (YYYY-MM-DD format)
   - Registration status (Current/Max)

**Example Output:**
```
--- Events ---
Event ID: 2001 | Name: Eid Festival | Date: 2026-04-29 | Registered: 150/500
Event ID: 2002 | Name: Bake Sale | Date: 2026-05-03 | Registered: 50/200
Event ID: 2003 | Name: Chand Raat | Date: 2026-05-01 | Registered: 80/300
Event ID: 2004 | Name: Basant Kite Festival | Date: 2026-03-21 | Registered: 0/1000
Event ID: 2005 | Name: Holi Color Festival | Date: 2026-03-17 | Registered: 200/800
```

---

#### **4. Book Ticket for Visitor**

**Purpose:** Purchase ride tickets for visitors

**Steps:**
1. Select option "4" from Staff Menu
2. System shows all visitors
3. Enter Visitor ID
4. System shows all operational rides
5. Enter Ride ID
6. Choose discount option:
   - Option 1: Apply 10% student discount
   - Option 2: No discount
7. Ticket is booked and saved

**Example Flow:**
```
--- Visitors ---
Visitor ID: 1 | Name: Abbas | Age: 28 | Email: abbas@email.com
Visitor ID: 2 | Name: Taher | Age: 25 | Email: taher@email.com
...

Enter Visitor ID: 1

--- Rides ---
Ride ID: 1 | Name: Roller Coaster | Price: $150.00 | Status: Operational
...

Enter Ride ID: 1
Apply student discount 10%? (1 Yes, 2 No): 1

Ticket booked successfully.
Ticket ID: 1001 | Visitor ID: 1 | Ride ID: 1 | Amount: $135.00
```

**Error Handling:**
- If Visitor ID not found: "Visitor ID not found"
- If Ride ID not found: "Ride ID not found"
- If ride in maintenance: "Ride is currently under maintenance"

**Data Storage:** Saved to `Tickets.txt`

---

#### **5. View All Visitors**

**Purpose:** See complete visitor list

**Steps:**
1. Select option "5" from Staff Menu
2. System displays all registered visitors

**Example Output:**
```
--- Visitors ---
Visitor ID: 1 | Name: Abbas | Age: 28 | Email: abbas@email.com
Visitor ID: 2 | Name: Taher | Age: 25 | Email: taher@email.com
Visitor ID: 3 | Name: Fatima | Age: 22 | Email: fatima@email.com
```

---

#### **6. Logout**

**Purpose:** Exit Staff Portal

**Steps:**
1. Select option "6"
2. Returns to main login menu

---

## Manager Portal - Complete Guide

### Access Requirements
- **Username:** `manager1`
- **Password:** `admin123`
- **Role:** Manager

### Manager Portal Menu

```
=== Manager Menu ===
1. Add Staff Member
2. Add Ride
3. Add Event
4. Add Inventory Item
5. Update Ride
6. Update Event
7. Update Inventory
8. Update Staff
9. Update Visitor
10. Update Ticket
11. View Feedback
12. View Revenue Report
13. View All Staff
14. View All Rides
15. View All Events
16. View All Inventory
17. Save Data
18. Logout
```

### What Manager Can Do - Detailed

#### **1. Add Staff Member**

**Purpose:** Hire new staff

**Steps:**
1. Select option "1" from Manager Menu
2. Enter staff member name
3. Enter role (Manager/Operator/Guide)
4. Enter monthly salary (0-100000)
5. System auto-generates Staff ID (starts at 3001)

**Example:**
```
Enter staff name: Hassan Ali
Enter role (Manager/Operator/Guide): Manager
Enter monthly salary: 45000.00

✓ Staff member added.

New Staff ID: 3001
```

**Data Storage:** Saved to `Staff.txt`

**Format:** `StaffID|Name|Role|Salary`

---

#### **2. Add Ride**

**Purpose:** Add new rides to the park

**Steps:**
1. Select option "2" from Manager Menu
2. Enter ride name
3. Enter ride price (0.00-10000.00)
4. Select status (1 = Operational, 2 = Maintenance)
5. System auto-generates Ride ID (starts at 1)

**Example:**
```
Enter ride name: Roller Coaster
Enter ride price: 150.00
Status (1 Operational, 2 Maintenance): 1

✓ Ride added.

New Ride ID: 1
```

**Data Storage:** Saved to `Rides.txt`

**Format:** `RideID|Name|Price|Operational(1/0)`

---

#### **3. Add Event**

**Purpose:** Schedule special events

**Steps:**
1. Select option "3" from Manager Menu
2. Enter event name
3. Enter event date (format: YYYY-MM-DD)
4. Enter event capacity (max visitors)
5. System auto-generates Event ID (starts at 2001)

**Example:**
```
Enter event name: Eid Festival
Enter event date (YYYY-MM-DD): 2026-04-29
Enter capacity: 500

✓ Event added.

New Event ID: 2001
```

**Data Storage:** Saved to `Events.txt`

**Format:** `EventID|Name|Date|Capacity|Registered`

**Sample Events in System:**
- Eid Festival (2026-04-29) - Capacity: 500
- Bake Sale (2026-05-03) - Capacity: 200
- Chand Raat (2026-05-01) - Capacity: 300
- Basant Kite Festival (2026-03-21) - Capacity: 1000
- Holi Color Festival (2026-03-17) - Capacity: 800

---

#### **4. Add Inventory Item**

**Purpose:** Track food, merchandise, and supplies

**Steps:**
1. Select option "4" from Manager Menu
2. Enter item name
3. Enter quantity (0-100000)
4. Enter cost per item (0.00-1000.00)
5. System auto-generates Inventory ID (starts at 4001)

**Example:**
```
Enter item name: Popcorn
Enter quantity: 150
Enter cost per item: 2.50

✓ Inventory item added.

New Inventory ID: 4001
```

**Data Storage:** Saved to `Inventory.txt`

**Format:** `InventoryID|ItemName|Quantity|CostPerItem`

---

#### **5. Update Ride**

**Purpose:** Update ride name, fare, or status

**Steps:**
1. Select option "5"
2. Choose update type (name, price, status, or all)
3. Enter updated values

---

#### **6. Update Event**

**Purpose:** Update event name, date, or capacity

**Steps:**
1. Select option "6"
2. Choose update type (name, date, capacity, or all)
3. Enter updated values
4. Capacity cannot be less than registered visitors

---

#### **7. Update Inventory**

**Purpose:** Update inventory name, quantity, or cost

**Steps:**
1. Select option "7"
2. Choose update type (name, quantity, cost, or all)
3. Enter updated values

---

#### **8. Update Staff**

**Purpose:** Update staff name, role, or salary

**Steps:**
1. Select option "8"
2. Choose update type (name, role, salary, or all)
3. Enter updated values

---

#### **9. Update Visitor**

**Purpose:** Update visitor name, age, or email

**Steps:**
1. Select option "9"
2. Choose update type (name, age, email, or all)
3. Enter updated values

---

#### **10. Update Ticket**

**Purpose:** Update ticket visitor, ride, or amount

**Steps:**
1. Select option "10"
2. Choose update type (visitor, ride, amount, or all)
3. Enter updated values (ride update re-validates operational status)

---

#### **11. View Feedback**

**Purpose:** Read visitor feedback and see ratings

**Steps:**
1. Select option "11" from Manager Menu
2. System displays all feedback entries
3. Shows average rating calculation

**Example Output:**
```
--- Feedback ---
Feedback ID: 5001 | Visitor: 1 | Rating: 5/5 | Comment: Amazing experience! Worth every penny
Feedback ID: 5002 | Visitor: 2 | Rating: 4/5 | Comment: Great rides, but lines were long
Feedback ID: 5003 | Visitor: 3 | Rating: 5/5 | Comment: Perfect event, loved the atmosphere
Feedback ID: 5004 | Visitor: 4 | Rating: 3/5 | Comment: Good but need better food options
Feedback ID: 5005 | Visitor: 5 | Rating: 5/5 | Comment: Best day ever with family!

Average Rating: 4.40/5
```

**Data Storage:** Loaded from `Feedback.txt`

**Format:** `FeedbackID|VisitorID|Rating|Comment`

---

#### **12. View Revenue Report**

**Purpose:** Generate financial reports

**Steps:**
1. Select option "12" from Manager Menu
2. System calculates and displays:
   - Total Ticket Revenue (from all tickets sold)

**Example Output:**
```
===== REVENUE REPORT =====
Total Ticket Revenue: $1,545.00
```

**Calculation Logic:**
```
Revenue = Sum of all ticket amounts
```

**Use Case:** Financial planning and business analysis

---

#### **13. View All Staff**

**Purpose:** See all staff members and their details

**Steps:**
1. Select option "13" from Manager Menu
2. System displays all staff with:
   - Staff ID
   - Name
   - Role
   - Salary

**Example Output:**
```
--- Staff Members ---
Staff ID: 3001 | Name: Hassan Ali | Role: Manager | Salary: $45000.00
Staff ID: 3002 | Name: Amina Khan | Role: Operator | Salary: $25000.00
Staff ID: 3003 | Name: Omar Sheikh | Role: Guide | Salary: $20000.00
Staff ID: 3004 | Name: Layla Ahmed | Role: Security | Salary: $22000.00
Staff ID: 3005 | Name: Karim Hassan | Role: Maintenance | Salary: $23000.00
```

---

#### **14. View All Rides**

**Purpose:** See all rides and their details

**Steps:**
1. Select option "14" from Manager Menu
2. System displays all rides

**Example Output:**
```
--- Rides ---
Ride ID: 1 | Name: Roller Coaster | Price: $150.00 | Status: Operational
Ride ID: 2 | Name: Ferris Wheel | Price: $100.00 | Status: Operational
Ride ID: 3 | Name: Bumper Cars | Price: $75.00 | Status: Operational
Ride ID: 4 | Name: Log Flume | Price: $120.00 | Status: Operational
Ride ID: 5 | Name: Teacup Ride | Price: $50.00 | Status: Operational
```

---

#### **15. View All Events**

**Purpose:** See all scheduled events

**Steps:**
1. Select option "15" from Manager Menu
2. System displays all events

**Example Output:**
```
--- Events ---
Event ID: 2001 | Name: Eid Festival | Date: 2026-04-29 | Registered: 150/500
Event ID: 2002 | Name: Bake Sale | Date: 2026-05-03 | Registered: 50/200
Event ID: 2003 | Name: Chand Raat | Date: 2026-05-01 | Registered: 80/300
Event ID: 2004 | Name: Basant Kite Festival | Date: 2026-03-21 | Registered: 0/1000
Event ID: 2005 | Name: Holi Color Festival | Date: 2026-03-17 | Registered: 200/800
```

---

#### **16. View All Inventory**

**Purpose:** Check stock levels

**Steps:**
1. Select option "16" from Manager Menu
2. System displays all inventory items

**Example Output:**
```
--- Inventory ---
Inventory ID: 4001 | Item: Popcorn | Quantity: 150 | Cost per Item: $2.50
Inventory ID: 4002 | Item: Ice Cream | Quantity: 200 | Cost per Item: $1.50
Inventory ID: 4003 | Item: Soft Drinks | Quantity: 300 | Cost per Item: $1.75
Inventory ID: 4004 | Item: Cotton Candy | Quantity: 100 | Cost per Item: $3.00
Inventory ID: 4005 | Item: Park Merchandise | Quantity: 50 | Cost per Item: $15.00
```

---

#### **17. Save Data**

**Purpose:** Manually save all data to files (auto-saved on logout)

**Steps:**
1. Select option "17" from Manager Menu
2. System saves all data:
   - ✓ Visitors to Visitors.txt
   - ✓ Rides to Rides.txt
   - ✓ Tickets to Tickets.txt
   - ✓ Events to Events.txt
   - ✓ Staff to Staff.txt
   - ✓ Feedback to Feedback.txt
   - ✓ Inventory to Inventory.txt
   - ✓ Users to Users.txt

**Output:**
```
✓ Data saved.
```

---

#### **18. Logout**

**Purpose:** Exit Manager Portal

**Steps:**
1. Select option "18"
2. Auto-saves data
3. Returns to main login menu

---

## Program Flow & Architecture

### High-Level Program Flow

```
START
  ↓
ThemeParkSystem Constructor
  ├─→ loadData() [Read 8 data files]
  ├─→ initializeDefaultUsers() [Create staff1 & manager1 if first run]
  └─→ app.run()
  ↓
Main Menu Loop
  ├─→ Option 1: login("Staff") → staffPortal()
  ├─→ Option 2: login("Manager") → managerPortal()
  └─→ Option 0: Exit → saveData() → END
  ↓
LOGIN PROCESS
  1. Request username
  2. Request password
  3. Validate against users vector
  4. Check role matches selected portal
  5. Set currentUser pointer
  6. Enter portal if successful
  ↓
STAFF/MANAGER PORTAL LOOP
  Display menu → Get choice → Execute action → Repeat/Logout
  ↓
Logout Process
  1. Set currentUser to nullptr
  2. Return to main menu (OR exit if manager)
  3. Auto-save all data
  ↓
ThemeParkSystem Destructor
  └─→ saveData() [Write 8 data files]
  ↓
END
```

### Data Flow During Ticket Booking (Most Complex Operation)

```
Staff: "Book Ticket" (Option 4)
  ↓
Show All Visitors (load from vector)
  ↓
Input: Visitor ID
  ↓
findById<Visitor>(visitorId) [Lambda search]
  ├─→ Found? Continue : Throw error
  ↓
Show All Rides (status = operational only)
  ↓
Input: Ride ID
  ↓
findById<Ride>(rideId)
  ├─→ Found? Continue : Throw error
  ├─→ Operational? Continue : Throw error
  ↓
Create Ticket object
  ├─→ Auto-assign ID (Ticket::nextId++)
  ├─→ Set visitorId, rideId, amount (from ride.price)
  ↓
Input: Apply discount?
  ├─→ Yes: Call applyDiscount(ticket, 10.0) [Friend function modifies amount]
  ├─→ No: Keep original price
  ↓
tickets.push_back(ticket) [Add to vector]
  ↓
Output: Ticket confirmation
  ↓
AUTO-SAVE (on logout/exit)
  └─→ serialize() each ticket to Tickets.txt
```

---

## Data Structure & File Format

### All Data Files (Pipe-Delimited Format)

All data files use `|` (pipe character) as separator for easy parsing.

#### **1. Visitors.txt**
```
Format: VisitorID|Name|Age|Email
Example:
1|Abbas|28|abbas@email.com
2|Taher|25|taher@email.com
3|Fatima|22|fatima@email.com
4|Ahmed|30|ahmed@email.com
5|Zainab|19|zainab@email.com
```

#### **2. Rides.txt**
```
Format: RideID|Name|Price|Operational(1=true, 0=false)
Example:
1|Roller Coaster|150.00|1
2|Ferris Wheel|100.00|1
3|Bumper Cars|75.00|1
4|Log Flume|120.00|1
5|Teacup Ride|50.00|1
```

#### **3. Events.txt**
```
Format: EventID|Name|Date|Capacity|Registered
Example:
2001|Eid Festival|2026-04-29|500|150
2002|Bake Sale|2026-05-03|200|50
2003|Chand Raat|2026-05-01|300|80
2004|Basant Kite Festival|2026-03-21|1000|0
2005|Holi Color Festival|2026-03-17|800|200
```

#### **4. Staff.txt**
```
Format: StaffID|Name|Role|Salary
Example:
3001|Hassan Ali|Manager|45000.00
3002|Amina Khan|Operator|25000.00
3003|Omar Sheikh|Guide|20000.00
3004|Layla Ahmed|Security|22000.00
3005|Karim Hassan|Maintenance|23000.00
```

#### **5. Tickets.txt**
```
Format: TicketID|VisitorID|RideID|Amount
Example:
1001|1|1|150.00
1002|2|2|100.00
1003|3|3|75.00
1004|4|4|120.00
1005|5|5|50.00
```

#### **6. Feedback.txt**
```
Format: FeedbackID|VisitorID|Rating|Comment
Example:
5001|1|5|Amazing experience! Worth every penny
5002|2|4|Great rides, but lines were long
5003|3|5|Perfect event, loved the atmosphere
5004|4|3|Good but need better food options
5005|5|5|Best day ever with family!
```

#### **7. Inventory.txt**
```
Format: InventoryID|ItemName|Quantity|CostPerItem
Example:
4001|Popcorn|150|2.50
4002|Ice Cream|200|1.50
4003|Soft Drinks|300|1.75
4004|Cotton Candy|100|3.00
4005|Park Merchandise|50|15.00
```

#### **8. Users.txt**
```
Format: UserID|Username|Password|Role
Example:
1001|staff1|pass123|Staff
2001|manager1|admin123|Manager
```

---

## Sample Data

### Complete Sample Dataset Included

The system comes pre-loaded with sample data:

**Visitors (5):**
- Abbas (28)
- Taher (25)
- Fatima (22)
- Ahmed (30)
- Zainab (19)

**Rides (5):**
- Roller Coaster ($150)
- Ferris Wheel ($100)
- Bumper Cars ($75)
- Log Flume ($120)
- Teacup Ride ($50)

**Events (5):**
- Eid Festival (April 29, 2026)
- Bake Sale (May 3, 2026)
- Chand Raat (May 1, 2026)
- Basant Kite Festival (March 21, 2026)
- Holi Color Festival (March 17, 2026)

**Staff (5):**
- Hassan Ali (Manager - $45,000)
- Amina Khan (Operator - $25,000)
- Omar Sheikh (Guide - $20,000)
- Layla Ahmed (Security - $22,000)
- Karim Hassan (Maintenance - $23,000)

**Inventory (5):**
- Popcorn (150 units at $2.50)
- Ice Cream (200 units at $1.50)
- Soft Drinks (300 units at $1.75)
- Cotton Candy (100 units at $3.00)
- Park Merchandise (50 units at $15.00)

**Feedback (5):**
- All with 3-5 star ratings from visitors
- Average rating: 4.4/5 stars

---

## OOP Concepts Implementation

All 13 OOP concepts are implemented in this system:

### 1. **Class & Object**
- 11 classes (ConsoleColor, ParkEntity, 5 derived, Ticket, Feedback, User, ThemeParkSystem)
- Objects created and used throughout

### 2. **Encapsulation**
- `private` members in all classes
- Public getters for accessing data
- Example: `Visitor` has private `age`, `email` with getters

### 3. **Inheritance**
- Single inheritance: Visitor, Ride, Event, Staff, Inventory inherit from ParkEntity
- Multi-level not used; focused on simple hierarchy

### 4. **Polymorphism**
- Virtual functions: `display()` and `serialize()` in ParkEntity
- Override in all 5 derived classes
- Demonstrates runtime polymorphism

### 5. **Abstraction**
- Abstract base class: ParkEntity has pure virtual functions
- Cannot instantiate ParkEntity directly
- Defines interface for all park entities

### 6. **Constructor Overloading**
- Each class has 2 constructors:
  - One with auto-ID generation
  - One with specified ID (for loading from files)

### 7. **Operator Overloading**
- Ticket class overloads:
  - `+` operator (add ticket amounts)
  - `<` operator (compare amounts)
  - `<<` stream operator (print ticket)

### 8. **Friend Function**
- `applyDiscount()` - Friend of Ticket class (modifies private member)
- `operator<<()` - Friend stream operator
- `calculateAverageRating()` - Friend of Feedback class

### 9. **Static Members**
- Each entity class has `static int nextId`
- Used for auto-incrementing IDs
- Example: `Visitor::nextId` starts at 1

### 10. **Template Function**
- `readNumber<T>()` - Generic template for input validation
- `findById<T>()` - Generic template for searching vectors
- Used for multiple data types

### 11. **STL Containers**
- `vector<Visitor>` - Dynamic array of visitors
- `vector<Ride>` - Dynamic array of rides
- `vector<Ticket>` - Dynamic array of tickets
- `vector<Event>` - Dynamic array of events
- `vector<Staff>` - Dynamic array of staff
- `vector<Feedback>` - Dynamic array of feedback
- `vector<Inventory>` - Dynamic array of inventory
- `vector<User>` - Dynamic array of users

### 12. **Lambda Functions**
- Used in `find_if()` algorithm in `findById()`
- Lambda: `[id](const T &item) { return item.getId() == id; }`

### 13. **Exception Handling**
- `try-catch` blocks in main portals
- `throw` statements for errors:
  - `invalid_argument()` - For invalid discount
  - `runtime_error()` - For not found/full event/insufficient inventory
- Graceful error recovery

---

## Quick Reference Summary

| Aspect | Details |
|--------|---------|
| **Language** | C++17 (Windows console) |
| **Compilation** | `g++ ThemeParkProject.cpp -std=c++17 -o ThemeParkProject.exe` |
| **Run Command** | `ThemeParkProject.exe` |
| **Total Classes** | 11 classes |
| **Total Data Files** | 8 files (pipe-delimited text) |
| **Default Users** | 2 (1 Staff + 1 Manager) |
| **Max Visitors** | 999 (IDs 1-999) |
| **ID Generation** | Auto-incremented static counters (no enforced max) |

---

## Troubleshooting Guide

| Issue | Solution |
|-------|----------|
| Program won't start | Check all 8 .txt files exist in themepark folder |
| Login fails | Verify username/password (case-sensitive) |
| Ticket booking fails | Ensure visitor and ride IDs exist |
| Ride unavailable | Ride status is "Maintenance"; manager can add operational ride |
| Data not saving | Program auto-saves on logout; manually use option 17 in manager portal |
| Colors not showing | Program uses Windows console API; may need Windows 7+ |

---

## Contact & Support

For questions or modifications, refer to the code comments in `ThemeParkProject.cpp`.

**Created:** April 27, 2026  
**Version:** 1.0  
**Status:** Production Ready  

