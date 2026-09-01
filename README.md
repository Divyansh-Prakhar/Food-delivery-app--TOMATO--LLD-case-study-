# Food Delivery System — Low Level Design

A Low-Level Design (LLD) implementation of a food delivery system using **Object-Oriented Design, SOLID principles, and Design Patterns** in C++.

The system models core food-ordering workflows including restaurant discovery, menu management, cart management, order creation, order types, payment processing, and notifications.

## Overview

The system is designed with extensibility and separation of responsibilities in mind. It uses abstraction and polymorphism to support different order types, payment methods, and order creation strategies.

### Core Components

- **User** — Represents a customer and maintains their cart.
- **Cart** — Manages selected menu items and calculates the total.
- **Restaurant** — Represents a restaurant and its menu.
- **MenuItem** — Represents an item available on a restaurant's menu.
- **Order** — Represents a customer's order.
- **DeliveryOrder** — Handles delivery-based orders.
- **PickupOrder** — Handles restaurant pickup orders.
- **OrderManager** — Manages the collection of orders.
- **RestaurantManager** — Manages restaurants and restaurant lookup.
- **NotificationService** — Handles order-related user notifications.
- **PaymentStrategy** — Abstraction for payment processing.

## Design Patterns

### Strategy Pattern — Payment

Payment processing is implemented using the Strategy Pattern.

```text
                 PaymentStrategy
                       |
          +------------+------------+
          |            |            |
      CreditCard    NetBanking      UPI
```

This allows new payment methods to be introduced without modifying the `Order` class or existing payment implementations.

### Factory Pattern — Order Creation

Order creation is abstracted using factories.

```text
                 IOrderFactory
                      |
             +--------+--------+
             |                 |
       NewOrderFactory   ScheduleOrderFactory
```

This keeps object creation separate from business logic and allows additional order creation workflows to be added independently.

### Singleton Pattern — Managers

The system uses Singleton for centralized managers:

- `RestaurantManager`
- `OrderManager`

This ensures a single shared instance manages the corresponding collection throughout the application lifecycle.

## Object-Oriented Design

The design makes use of:

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism
- Composition
- Association
- Dependency on interfaces rather than concrete implementations

`DeliveryOrder` and `PickupOrder` extend the base `Order` abstraction, allowing the system to work with different order types polymorphically.

## Order Flow

```text
User
 |
 v
Restaurant
 |
 v
Menu
 |
 v
Cart
 |
 v
Order
 |
 +-------------------+
 |                   |
 v                   v
DeliveryOrder     PickupOrder
 |
 v
PaymentStrategy
 |
 +-----------------------------+
 |             |               |
 v             v               v
CreditCard  NetBanking        UPI
 |
 v
NotificationService
```

## UML

The following UML class diagram represents the system design and relationships between its major components.

![UML Class Diagram](UML.png)

## SOLID Principles

The implementation follows the SOLID principles wherever applicable.

### Single Responsibility Principle

Responsibilities are separated across domain classes and services.

For example:

- `Cart` manages cart-related operations.
- `OrderManager` manages orders.
- `RestaurantManager` manages restaurants.
- `NotificationService` handles notifications.
- Payment implementations handle payment processing.

### Open/Closed Principle

The design allows new behaviors to be introduced through abstractions.

For example, a new payment method can implement `PaymentStrategy` without modifying existing payment implementations.

### Liskov Substitution Principle

Specialized order types such as `DeliveryOrder` and `PickupOrder` can be used wherever an `Order` is expected.

### Interface Segregation Principle

Interfaces such as `PaymentStrategy` and `IOrderFactory` expose focused responsibilities rather than large, unrelated contracts.

### Dependency Inversion Principle

Core components depend on abstractions such as:

- `PaymentStrategy`
- `IOrderFactory`

rather than directly depending on concrete implementations.

## Project Structure

```text
Food-Delivery-System/
│
├── include/
│   ├── User.h
│   ├── Cart.h
│   ├── Restaurant.h
│   ├── MenuItem.h
│   ├── Order.h
│   ├── DeliveryOrder.h
│   ├── PickupOrder.h
│   ├── PaymentStrategy.h
│   ├── CreditCard.h
│   ├── NetBanking.h
│   ├── UPI.h
│   ├── IOrderFactory.h
│   ├── NewOrderFactory.h
│   ├── ScheduleOrderFactory.h
│   ├── OrderManager.h
│   ├── RestaurantManager.h
│   └── NotificationService.h
│
├── src/
│   └── ...
│
├── UML.png
├── main.cpp
└── README.md
```

> The exact project structure may vary depending on the implementation.

## Tech Stack

- **Language:** C++
- **Paradigm:** Object-Oriented Programming
- **Design:** Low-Level Design (LLD)
- **Concepts:** SOLID, Design Patterns, Abstraction, Polymorphism
- **STL:** C++ Standard Template Library

## Key Design Goals

- **Maintainability** — Clear separation of responsibilities.
- **Extensibility** — New order types and payment methods can be added with minimal changes.
- **Loose Coupling** — Abstractions are preferred over concrete implementations.
- **Reusability** — Common behavior is represented through reusable interfaces and base classes.
- **Testability** — Isolated components make individual behaviors easier to test.

## Future Enhancements

- Restaurant ratings and reviews
- Delivery partner management
- Order status tracking
- Coupon and discount management
- Inventory management
- Payment transaction management
- User authentication
- Persistent storage
- REST API integration
- Concurrent order processing
- Observer-based notification system

## Purpose

This project demonstrates the practical application of **Object-Oriented Programming, SOLID principles, UML-based design, and common Design Patterns** in a real-world domain.

It serves as an LLD exercise and a foundation that can be extended toward a production-oriented food delivery architecture.
