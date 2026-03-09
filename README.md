# Hotel Booking Management System

## Original Authors
This project is created and maintained by:

* **Muhammad Amir Imran bin Abdul Razak** 
* **Akmal Hakimi bin Abd Rashid** 
* **Ahmad Aneq bin Mustapa** 
* **Amirul Aidil bin Amir Hasan** 
* **Muhammad Aiman bin Abdul Salim** 

## Introduction
**Hotel Booking Management System** is a Java Swing desktop application developed as part of the **ISB26504 - Software Design and Integration** course at **Universiti Kuala Lumpur (UniKL MIIT)** during the March 2025 session. The application serves as a hotel room reservation management system that supports multiple branches.

The goal of this project is to provide a fully functional desktop application that allows administrators to manage room availability, create bookings for customers, and maintain booking records — all through an intuitive graphical user interface. The system uses **in-memory data structures** for lightweight, fast data management without requiring an external database.

## Problem Statements & Objectives

### Problem Statements
* **Manual Booking Errors and Inefficiencies**: The existing methods of booking manually are susceptible to confirmation delays and oversights like double bookings, which creates dissatisfaction among customers and slows down operations.
* **Absence of Centralized Booking System**: Without an automated system, manually coordinating room availability and booking information becomes overly complicated, restricting the hotel's ability to track available inventory and service clients in a timely manner.
* **Lack of Data Persistence and Real-Time Access**: Existing methodologies provide no live updates on booking activities as well as no access to historical data, severely limiting effective customer service and decision making.
* **Limited Accessibility to Booking Modifications**: Dealing with duplicate bookings, changing reservations, or record deletions often require additional steps which increase workload and likelihood of errors.

### Objectives
* To develop an application that incorporates booking, administration, and viewing functionality in the form of a Java Swing graphical user interface
* To implement in-memory data structures for managing room bookings and availability using centralized data storage
* To allow management control for setting room availability thresholds
* To allow the creation, duplication, updating, and deletion of bookings (full CRUD operations)
* To ensure reliability by managing user input validation and exceptions without crashing the application or corrupting data
* To provide an application structure that adheres to the separation of concerns principle, organized modules, and reusable user interface components

## Program Scope
The Hotel Booking Management System allows users to:
* **Make New Bookings** — Fill in customer details, select branch, room type, check-in/out dates, and optional add-ons with a real-time price summary and room preview image
* **Admin Login** — Password-protected access to the admin dashboard for managing room availability
* **Set Room Availability** — Administrators can configure available room counts per room type (Suite, Deluxe, Standard)
* **View All Bookings** — Browse all bookings in a searchable, formatted table with 8 columns
* **Duplicate Bookings** — Clone existing bookings into a pre-filled editable form for quick re-booking
* **Edit Bookings** — Modify any field of a duplicated booking and save changes
* **Delete Bookings** — Remove bookings with a confirmation dialog
* **Search Bookings** — Filter bookings by any field using substring search

The application is built with **Java** (JDK 8+) using **Swing** and **AWT** for the graphical user interface, and **JDatePicker** for date selection.

## Room Types & Pricing

| Room Type | Price per Night | Image Preview |
| :--- | :--- | :--- |
| `Suite` | RM 200 | `lib/image/suite_image.jpg` |
| `Deluxe` | RM 150 | `lib/image/deluxe_image.jpg` |
| `Standard` | RM 100 | `lib/image/standard_image.jpg` |

### Optional Add-ons

| Add-on | Price |
| :--- | :--- |
| `Meals` | +RM 20 |
| `High-Speed WiFi` | +RM 10 |
| `Laundry` | +RM 15 |

### Hotel Branches

| Branch | Description |
| :--- | :--- |
| `CityHotel` | Urban city location |
| `BeachResort` | Coastal beach resort |

## Tech Stack

| Layer | Technology |
| :--- | :--- |
| `Language` | Java (JDK 8 or newer) |
| `GUI Framework` | Java Swing + AWT |
| `Date Picker` | JDatePicker 1.3.4 |
| `Data Handling` | In-memory static data structures (ArrayList, HashMap) |
| `Build Tool` | javac (manual compilation, no Maven/Gradle) |
| `IDE` | VS Code with Extension Pack for Java |
| `Security` | Password-based admin authentication |

### Dependencies

| Library | Version | Purpose |
| :--- | :--- | :--- |
| [JDatePicker](https://github.com/JDatePicker/JDatePicker) | 1.3.4 | Date picker UI component for check-in/out date selection |

## Prerequisites
* **Java Development Kit (JDK)** 8 or newer installed and added to your PATH
* **VS Code** with [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) (recommended) or any Java IDE
* No external database required — all data is managed in-memory

## Getting Started

1. **Clone or extract** the project to your local machine.

2. **Compile all sources:**
   ```bash
   javac -cp "lib/*" -d bin src/*.java
   ```

3. **Run the application:**
   ```bash
   java -cp "bin;lib/*" HotelSystemGUI
   ```

   > **Note:** On Linux/macOS, replace `;` with `:` in the classpath separator:
   > ```bash
   > java -cp "bin:lib/*" HotelSystemGUI
   > ```

4. **Using VS Code:**
   - Open the project folder in VS Code
   - The project is auto-configured via `.vscode/settings.json`
   - Run `HotelSystemGUI.java` using the **Run** button or `F5`

## Project Structure

```
GUIHOTELMANAGEMENT/
├── src/                              # Java source files
│   ├── HotelSystemGUI.java          # App entry point, home screen with navigation
│   ├── AdminLoginPanel.java         # Admin password authentication panel
│   ├── AdminPanel.java              # Room availability management panel
│   ├── BookingPanel.java            # New booking form with real-time summary
│   ├── BookingListPanel.java        # View all bookings in searchable table
│   ├── BookingStorage.java          # Centralized in-memory booking data store
│   ├── DuplicateBookingPanel.java   # Browse, select, duplicate & delete bookings
│   └── EditDuplicateBooking.java    # Edit duplicated booking with pre-filled form
├── lib/
│   ├── jdatepicker-1.3.4.jar        # Date picker component library
│   └── image/                        # Room type preview images
│       ├── suite_image.jpg
│       ├── deluxe_image.jpg
│       └── standard_image.jpg
├── bin/                              # Compiled .class output files
└── .vscode/
    └── settings.json                 # VS Code Java project configuration
```

### Class Diagram Structure
* **HotelSystemGUI (App Entry)**: Initializes the application via `SwingUtilities.invokeLater()`, displays home screen with 4 navigation buttons.
* **BookingStorage (Data Layer)**: Single class centralizing all booking data using a static `ArrayList<String>` with pre-loaded sample bookings.
* **AdminPanel (Admin Layer)**: Manages room availability through a static `HashMap<String, Integer>` accessible across all panels.
* **BookingPanel (Booking Form)**: Split-panel layout with form (left 60%) and real-time summary with room image (right 40%).

| Class | Responsibility |
| :--- | :--- |
| `HotelSystemGUI` | Application entry point (`main()`), home screen with 4 navigation buttons in a 2x2 grid layout |
| `BookingStorage` | Centralized in-memory data store for all bookings using static `List<String>` with `addBooking()`, `getBookings()`, and `getBooking()` methods |
| `AdminLoginPanel` | Password authentication gate with gradient background, Enter-key support, and navigation to `AdminPanel` on success |
| `AdminPanel` | Room availability management with dropdown selector, quantity input, and static `getAvailability()` method for cross-panel access |
| `BookingPanel` | New booking form with customer fields, JDatePicker for dates, branch/room selection, add-on checkboxes, real-time price summary, and room image preview |
| `BookingListPanel` | Displays all bookings in a formatted `JTable` with 8 columns, regex-based text parsing, substring search, and alternating row colors |
| `DuplicateBookingPanel` | Browse bookings via scrollable sidebar buttons, view details in center panel, duplicate to pre-filled form, or delete with confirmation |
| `EditDuplicateBooking` | Edit duplicated booking with pre-populated fields, real-time summary updates via `DocumentListener`, save replaces original or adds new booking |

## Data Schema

### In-Memory Data Structures

**`BookingStorage` — Static ArrayList\<String\>**

Each booking is stored as a formatted multi-line string with the following fields:

| Field | Type | Description |
| :--- | :--- | :--- |
| `Name` | String | Customer's full name |
| `Email` | String | Customer's email address (regex validated) |
| `Phone` | String | Customer's phone number |
| `Check-in Date` | String | Check-in date (yyyy-MM-dd format) |
| `Check-out Date` | String | Check-out date (yyyy-MM-dd format) |
| `Branch` | String | Hotel branch (CityHotel or BeachResort) |
| `Room Type` | String | Selected room type (Suite, Deluxe, or Standard) |
| `Add-ons` | String | Comma-separated add-on names or "None" |
| `Total Price` | String | Calculated total in RM |

**`AdminPanel.roomAvailability` — Static HashMap\<String, Integer\>**

| Key (Room Type) | Value (Quantity) | Default |
| :--- | :--- | :--- |
| `Suite` | Integer | 1 |
| `Deluxe` | Integer | 1 |
| `Standard` | Integer | 1 |

## Application Flow

```
┌─────────────────────────────────────────────────────────┐
│                    HotelSystemGUI                       │
│                    (Home Screen)                        │
│                                                         │
│  ┌─────────────────┐    ┌─────────────────────────┐    │
│  │  1. Make New    │    │  2. Admin: Set Room      │    │
│  │     Booking     │    │     Availability         │    │
│  └────────┬────────┘    └────────────┬─────────────┘    │
│           │                          │                   │
│  ┌────────▼────────┐    ┌────────────▼─────────────┐    │
│  │  3. Show All    │    │  4. Duplicate Booking     │    │
│  │     Bookings    │    │                           │    │
│  └────────┬────────┘    └────────────┬──────────────┘    │
└───────────┼──────────────────────────┼──────────────────┘
            │                          │
            ▼                          ▼
    ┌───────────────┐      ┌──────────────────────┐
    │  BookingPanel  │      │  AdminLoginPanel      │
    │  (New Booking  │      │  (Password Gate)      │
    │   Form)        │      └──────────┬────────────┘
    └───────────────┘                  │ Access Granted
                                       ▼
    ┌───────────────┐      ┌──────────────────────┐
    │BookingListPanel│      │     AdminPanel        │
    │ (Table View +  │      │  (Set Availability)   │
    │  Search)       │      └──────────────────────┘
    └───────────────┘
                               ┌──────────────────────┐
    ┌───────────────────┐      │  EditDuplicateBooking │
    │DuplicateBookingPanel│───▶│  (Pre-filled Edit     │
    │ (Browse/Delete)    │     │   Form)               │
    └───────────────────┘      └──────────────────────┘
```

### Navigation Routes

| Source | Destination | Trigger |
| :--- | :--- | :--- |
| `HotelSystemGUI` | `BookingPanel` | "Make New Booking" button |
| `HotelSystemGUI` | `AdminLoginPanel` | "Admin: Set Room Availability" button |
| `HotelSystemGUI` | `BookingListPanel` | "Show All Bookings" button |
| `HotelSystemGUI` | `DuplicateBookingPanel` | "Duplicate Booking" button |
| `AdminLoginPanel` | `AdminPanel` | Correct password entered |
| `DuplicateBookingPanel` | `EditDuplicateBooking` | "Duplicate Booking" button on selected booking |
| Any Panel | `HotelSystemGUI` | "Back to Home" button |

## Features

### Booking Features
* **New Booking Form** — Split-panel layout with form fields on the left (60%) and live summary with room image on the right (40%)
* **Real-Time Price Summary** — Total price updates dynamically as the user selects room type and add-ons via `KeyListener` and `ActionListener`
* **Room Image Preview** — Displays the corresponding room type image (Suite, Deluxe, or Standard) that updates on selection change
* **Date Selection** — JDatePicker component for check-in and check-out date selection with `yyyy-MM-dd` formatting
* **Input Validation** — Required field checks, email regex validation, check-in date cannot be in the past, check-out must be after check-in
* **Booking Storage** — Successfully submitted bookings are stored in `BookingStorage` with a confirmation dialog

### View & Search Features
* **Booking Table** — All bookings displayed in a formatted `JTable` with 8 columns (Name, Email, Phone, Date, Branch, Room Type, Add-ons, Price)
* **Alternating Row Colors** — Even/odd row color differentiation for readability
* **Search** — Filter bookings by typing any keyword; searches across all columns with case-insensitive substring matching
* **Non-Editable Table** — Table cells are read-only to prevent accidental data modification

### Duplicate & Edit Features
* **Booking Browser** — Scrollable sidebar with booking buttons showing "Booking #N - Name on Date"
* **Booking Details View** — Selected booking details displayed in the center panel
* **Duplicate Booking** — Opens `EditDuplicateBooking` form pre-filled with the selected booking's data for quick re-booking
* **Edit Booking** — Modify any field (name, email, phone, date, branch, room type, add-ons) with real-time summary updates
* **Delete Booking** — Remove a booking with a confirmation dialog before deletion

### Administrator Features
* **Password-Protected Access** — Admin login requires correct password before accessing the availability panel
* **Gradient Login UI** — Admin login panel features a gradient background for visual distinction
* **Room Availability Control** — Set available room count per room type (Suite, Deluxe, Standard) with validation for non-negative integers
* **Cross-Panel Availability Display** — Booking form shows current room availability fetched from `AdminPanel.getAvailability()`

## Screenshots Guide

### User Flow
1. **Home Screen** — Application launches with "Welcome to the Hotel Booking System" title and 4 navigation buttons in a 2x2 grid
2. **New Booking** — Split-panel form with customer details on the left and live booking summary with room image on the right
3. **Room Selection** — Room type dropdown updates the available count label and room preview image
4. **Date Selection** — JDatePicker popup for selecting check-in and check-out dates
5. **Add-ons** — Checkbox selection for Meals, High-Speed WiFi, and Laundry with real-time price recalculation
6. **Booking Confirmation** — Success dialog after booking submission
7. **View All Bookings** — Table view with all bookings, search bar at the top, and alternating row colors
8. **Search Results** — Filtered table showing only bookings matching the search term

### Admin Flow
1. **Admin Login** — Gradient-styled password prompt with Login and Back buttons
2. **Access Granted** — Success dialog before navigating to the admin panel
3. **Set Availability** — Dropdown for room type, quantity input field, and Update button
4. **Availability Updated** — Confirmation dialog showing updated room count

### Duplicate Flow
1. **Booking Browser** — Left sidebar with scrollable booking buttons, center panel with booking details
2. **Select Booking** — Click a booking button to view its full details
3. **Duplicate** — Opens edit form pre-filled with the selected booking's data
4. **Edit Fields** — Modify any field with real-time summary updates on the right
5. **Save** — Saves the edited booking and returns to the duplicate booking panel
6. **Delete** — Confirmation dialog before removing the selected booking

## Design Patterns & Principles

| Pattern / Principle | Implementation |
| :--- | :--- |
| `Centralized Data Store` | `BookingStorage` manages all booking data through static methods, providing a single source of truth across all panels |
| `Panel-Based Navigation` | Each feature is encapsulated in its own `JFrame`, promoting modularity and separation of functionality |
| `Real-Time UI Updates` | Booking summary and pricing update dynamically as users fill in the form via `DocumentListener`, `KeyListener`, and `ActionListener` |
| `Static Cross-Panel Access` | `AdminPanel.getAvailability()` provides static access to room availability data from any panel without instance references |
| `Input Validation` | Email regex validation (`^[A-Z0-9._%+-]+@[A-Z0-9.-]+\\.[A-Z]{2,6}$`), date constraint checks, and required field enforcement |

## Version History

| Version | Description |
| :--- | :--- |
| `Version 01` | Basic modules: Login Panel, Booking Panel, Set Room Availability, Show Booking Panel |
| `Version 02` | Enhanced UI with modern styling, Home Menu dashboard, Duplicate Booking module, search functionality, room images, and real-time summary |
| `Version 03 (Planned)` | Quick Search & Filter System, Loyalty Rewards System, Monthly Sales & Room Analytics with graphs |

## License

This project was developed for academic purposes as part of the **ISB26504 - Software Design and Integration** course at **Universiti Kuala Lumpur (UniKL MIIT)**.
