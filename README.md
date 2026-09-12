# Movie Ticket Booking System

A menu-driven **C++ console application** for a single cinema, built to practice Low-Level Design (LLD) and Object-Oriented Programming.

## Features

- View movies currently playing
- View shows for a chosen movie
- Display a live seat layout (Silver, Gold, Platinum) with availability
- Book one or more seats; reject invalid, taken, or duplicate seats
- Calculate ticket price dynamically by seat category
- Pay via UPI, Card, or Cash
- Roll back and free seats if payment is declined
- Print a formatted ticket after a successful booking
- Cancel a booking, release its seats, and issue a refund
- Look up past bookings by Booking ID or phone number

## Prices

- SILVER: Rs. 150
- GOLD: Rs. 250
- PLATINUM: Rs. 400

## File Structure

One class per `.cpp` file, no header files:

```
MovieTicketBookingSystem/
├── main1.cpp             # Entry point, sets up cinema/movies/shows
├── movie2.cpp            # Movie
├── seat3.cpp             # Seat
├── screen4.cpp           # Screen
├── cinema5.cpp           # Cinema
├── showSeat6.cpp         # ShowSeat (per-show seat status)
├── show7.cpp             # Show
├── priceCalculator8.cpp  # PriceCalculator
├── bookingService9.cpp   # Booking + BookingService (app flow)
├── customer10.cpp        # Customer
├── payment11.cpp         # Payment (abstract base)
├── upiPayment12.cpp      # UpiPayment
├── cardPayment13.cpp     # CardPayment
├── cashPayment14.cpp     # CashPayment
├── docs/                 # Diagrams and design docs
└── README.md
```

## Compile and Run

```bash
g++ main1.cpp -o MovieTicketBooking
```

**Windows:**
```powershell
.\MovieTicketBooking.exe
```

**macOS/Linux:**
```bash
./MovieTicketBooking
```

## OOP Concepts Used

- **Encapsulation** — every class keeps its data `private` and exposes only getters/behavior (e.g. `ShowSeat` only lets you `bookSeat()`/`releaseSeat()`, never touch status directly)
- **Abstraction** — `Payment` is a pure abstract class; it declares `pay()` and `getPaymentType()` without defining how
- **Inheritance** — `UpiPayment`, `CardPayment`, `CashPayment` each extend `Payment`
- **Runtime polymorphism** — `BookingService::processPayment(Payment&, double)` calls the correct `pay()` for whichever payment type is passed in
- **Composition** — `Cinema` owns `Screen`s, `Screen` owns `Seat`s, `Show` owns `ShowSeat`s — none of these exist independently of their parent
- **Aggregation** — `Show` references a `Movie` by pointer; `Booking` references the `ShowSeat`s it booked
- **Association** — `BookingService` coordinates `Customer`, `Show`, and `Payment` without owning them

## System Diagrams

See `docs/` for the end-to-end workflow flowchart, UPI payment sequence diagram, and architecture diagram, plus PDFs covering requirements analysis, noun-verb analysis, class design, object relationships, SOLID principles, and UML.
