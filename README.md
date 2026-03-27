# COMP1035 Software Engineering — Coursework 1

## ShopEase E-Commerce Mobile Application: Requirements & Specifications Report

---

## Table of Contents

- [COMP1035 Software Engineering — Coursework 1](#comp1035-software-engineering--coursework-1)
  - [ShopEase E-Commerce Mobile Application: Requirements \& Specifications Report](#shopease-e-commerce-mobile-application-requirements--specifications-report)
  - [Table of Contents](#table-of-contents)
  - [Part A: User Requirements](#part-a-user-requirements)
    - [1. Textual Analysis](#1-textual-analysis)
      - [1.1 Actors](#11-actors)
      - [1.2 Use Cases](#12-use-cases)
    - [2. Use Case Diagram](#2-use-case-diagram)
    - [3. Personas](#3-personas)
      - [Persona 1: Chloe Davis — Buyer](#persona-1-chloe-davis--buyer)
      - [Persona 2: Jonathan Patterson — Seller](#persona-2-jonathan-patterson--seller)
      - [Persona 3: Mei Lin — Administrator](#persona-3-mei-lin--administrator)
  - [Part B: System Requirements (Specifications)](#part-b-system-requirements-specifications)
    - [4. Activity Diagram](#4-activity-diagram)
    - [5. Low-Fidelity Prototype](#5-low-fidelity-prototype)
  - [Notes, Queries \& Assumptions](#notes-queries--assumptions)
    - [Notes](#notes)
    - [Queries for the Client (Mei Lin)](#queries-for-the-client-mei-lin)
    - [Assumptions](#assumptions)

---

## Part A: User Requirements
 
### 1. Textual Analysis
 
#### 1.1 Actors
 
| Actor | Extracted Text | Description |
|-------|---------------|-------------|
| **Buyer** | *"...allow buyers to browse products, filter by categories, read reviews, make secure payments, and track orders in real time."* | End-users who search for products, make purchases, write reviews, and track deliveries. |
| **Seller** | *"Sellers will have access to a dashboard to manage inventory, process orders, and communicate with customers."* | Independent business owners who manage product listings, fulfil orders, and access sales analytics. |
| **Administrator** | *"The platform administrator, representing ShopEase, has the responsibility of overseeing the entire ecosystem."* | ShopEase staff responsible for approving sellers, resolving disputes, managing categories/promotions, and monitoring performance. |
 
**Rationale:** Three distinct human roles with different permissions and goals. Payment processing is handled internally through the Make Payment use case, integrating with a third-party provider behind the scenes.
 
#### 1.2 Use Cases
 
| Use Case | Extracted Text | Description |
|----------|---------------|-------------|
| **Log In** | *"They need to be able to register and log in securely..."* | Secure authentication for all users. Also covers account registration. |
| **Browse Products** | *"The app will allow buyers to browse products, filter by categories..."* | Buyers explore the catalogue through listings, categories, and recommendations. |
| **Search Products** | *"...search for products using various filters such as category, price range, and customer ratings..."* | Optional refinement of browsing via search keywords and filters. Extends Browse Products. |
| **Manage Cart** | *"...they should be able to add them to a shopping cart..."* | Buyers add, update, or remove items before checkout. |
| **Checkout Order** | *"...proceed through a secure checkout process."* | Buyer confirms cart, enters shipping details, completes purchase. Includes Make Payment and Log In. |
| **Make Payment** | *"...make secure payments..."* | Payment processed through external gateway. Mandatory step within Checkout Order. |
| **Track Order** | *"...track their orders in real time..."* / *"...view their order history."* | Live order status and past order records. |
| **Write Review** | *"...view detailed product information including images and reviews."* | Ratings and reviews for purchased products. Optionally extends Track Order. |
| **Send Message** | *"...communicate directly with buyers through an in-app messaging system."* | In-app messaging between Buyers and Sellers. |
| **Manage Product Listings** | *"...easily add new products, update existing listings, and remove items..."* / *"...view and manage incoming orders..."* / *"...sales reports and analytics..."* | Sellers manage products, process orders, and view analytics. |
| **Approve Seller** | *"The administrator needs tools to approve new seller registrations..."* | Administrator reviews and approves/rejects seller applications. |
| **Manage Platform** | *"...monitor platform activity..."* / *"...manage product categories, create promotional campaigns, and configure platform settings."* | Administrator oversees disputes, categories, promotions, settings, and reports. |
 
**Rationale:** Consolidated into 12 high-level use cases for clarity. Register Account merged into Log In; View Order History into Track Order; Process Orders and View Sales Analytics into Manage Product Listings; all admin operations into Manage Platform.
 
---
 
### 2. Use Case Diagram
 
Three actors (Buyer, Seller, Administrator) interact with 12 use cases within the system boundary.
 

 
![Use Case Diagram](images/use_case_diagram.png)
 
---

### 3. Personas

The following three personas represent the primary user types of the ShopEase application. Each persona is grounded in the requirements brief and designed to guide development decisions by capturing realistic goals, frustrations, and behavioural traits.

> **Rationale:** We created one persona per primary actor (Buyer, Seller, Administrator) to ensure that all user perspectives are represented. The personas reflect the brief's emphasis on mobile-first design for buyers, dashboard simplicity for sellers, and comprehensive oversight tools for administrators.

#### Persona 1: Chloe Davis — Buyer

![Persona: Jia Wen Lim (Buyer)](images/persona_buyer.png)

**Connection to requirements:** Chloe directly represents the Buyer actor in the use case diagram. Her goals (browsing, secure checkout, real-time tracking, personalised recommendations) map to the use cases: Browse Products, Search Products, Manage Cart, Checkout Order, Track Order, View Order History, and Receive Notifications. Her frustration with the current website validates Mei Lin's vision for a dedicated mobile application.

---

#### Persona 2: Jonathan Patterson — Seller

![Persona: Arjun Nair (Seller)](images/persona_seller.png)

**Connection to requirements:** Jonathan represents the Seller actor. His goals (managing listings, processing orders, communicating with buyers) map to the use cases: Manage Product Listings, Process Orders, View Sales Analytics, and Send Message. His moderate tech proficiency reinforces the brief's requirement that the system must be user-friendly with minimal training.

---

#### Persona 3: Mei Lin — Administrator

![Persona: Rachel Okonkwo (Administrator)](images/persona_admin.png)

**Connection to requirements:** Mei Lin represents the Administrator actor. Her goals (approving sellers, resolving disputes, monitoring KPIs, managing promotions) map to the use cases: Approve Seller, Resolve Disputes, Manage Categories, Create Promotions, View Platform Reports, and Configure Settings. Her need for comprehensive reporting aligns with the brief's emphasis on strategic decision-making.

---

## Part B: System Requirements (Specifications)

### 4. Activity Diagram

The activity diagram below models the **"Checkout Order"** use case, which was selected because it is one of the most critical and complex workflows in the ShopEase application. This use case involves all three swimlane participants (Buyer, ShopEase System, and Payment Gateway), includes decision points, parallel activities, and integrates with the Make Payment use case via the <<include>> relationship identified in the use case diagram.

**Rationale for choosing Checkout Order:**
- It is central to ShopEase's core business function (completing purchases).
- It involves multiple actors across the system boundary (Buyer, System, and the external Payment Gateway).
- It demonstrates decision logic (item availability, payment approval/failure).
- It includes parallel processing (generating the order and sending confirmation simultaneously).
- It connects clearly to the use case diagram (Checkout Order <<include>> Make Payment).

**Key elements of the activity diagram:**
- **Swimlanes** separate responsibilities: the Buyer provides input and decisions, the ShopEase System handles validation and processing, and the Payment Gateway verifies payment.
- **Decision nodes** handle two conditional branches: whether cart items are available, and whether payment is approved.
- **Fork and join bars** model parallel activities after payment confirmation — the system simultaneously generates the order record and sends a confirmation notification to the buyer.
- **Initial and final nodes** clearly mark the start and end of the process.

![Activity Diagram: Checkout Order](images/activity_diagram.png)

---

### 5. Low-Fidelity Prototype

The low-fidelity prototype below illustrates the **Buyer shopping flow**, covering the use cases: Browse Products → View Product Details → Manage Cart → Checkout Order → Order Confirmation (with Track Order). This flow was chosen because it represents the primary user journey through the application and aligns directly with Mei Lin's vision of a modern, intuitive shopping platform.

**Rationale for choosing this flow:**
- It covers the end-to-end buyer experience, which is the most important user journey for ShopEase.
- It demonstrates the mobile-first design that Mei Lin specifically requested (no spreadsheets, no basic forms).
- It integrates multiple use cases from the use case diagram into a cohesive visual narrative.
- It connects directly to the activity diagram: screens 3–5 (Cart → Checkout → Confirmation) mirror the Checkout Order activity flow.

**Key design decisions:**
- **Screen 1 (Home):** Personalised recommendations and promotional banners address the brief's requirement for personalised product recommendations and promotions. Category chips provide quick filtering.
- **Screen 2 (Product Details):** Includes seller information, customer reviews, star ratings, and a prominent "Add to Cart" button — covering the brief's requirement for detailed product information.
- **Screen 3 (Shopping Cart):** Displays quantity controls, pricing breakdown, and two clear call-to-action buttons. Meets Mei Lin's desire for an intuitive, not spreadsheet-like, interface.
- **Screen 4 (Checkout):** Shows shipping address, multiple payment options (credit card, e-wallet, bank transfer), and an order summary. The lock icon signals secure payment processing.
- **Screen 5 (Order Confirmation):** Provides order tracking status with a visual progress indicator, estimated delivery, and navigation options — addressing the real-time tracking requirement.

![Low-Fidelity Prototype: Buyer Shopping Flow](images/prototype.png)

---

## Notes, Queries & Assumptions
 
### Notes
1. **Integration between diagrams:** The same actors (Buyer, Seller, Administrator) appear consistently across the textual analysis, use case diagram, personas, activity diagram, and prototype. For example, the "Checkout Order" use case appears in the textual analysis, is shown in the use case diagram with its <<include>> relationship to Make Payment, is modelled step-by-step in the activity diagram, and is visually represented in prototype screens 3–5.
2. **Scope of third-party integrations:** Payment processing relies on a third-party gateway integrated within the Make Payment use case. Future iterations may include external notification services (push notifications, SMS) and shipping/logistics APIs.
3. **Persona diversity:** The three personas represent different geographies, age groups, tech proficiencies, and user goals to ensure the design caters to a diverse user base.
 
### Queries for the Client (Mei Lin)
1. Should sellers be required to provide business registration documents during the approval process, or is basic identity verification sufficient?
2. What payment gateways should be prioritised for the initial launch (e.g., Stripe, PayPal, local e-wallets)?
3. Is there a preferred dispute resolution process (e.g., automated refund rules, manual administrator review, or a combination)?
4. Should buyers be able to save multiple shipping addresses, or is a single default address sufficient for the first release?
5. Are there any specific sales analytics metrics that sellers have requested beyond revenue, popular products, and customer activity?
 
### Assumptions
1. **Authentication:** We assume the system will use email/password authentication with optional multi-factor authentication, as mentioned in the system qualities section of the brief.
2. **Payment processing:** All payments are handled by a third-party payment gateway; ShopEase does not process or store card details directly.
3. **Real-time tracking:** Order tracking data is updated by sellers when they change order statuses (e.g., shipped, delivered) rather than through GPS-based live tracking.
4. **Messaging scope:** The in-app messaging system supports text-based communication between buyers and sellers; file/image sharing may be a future enhancement.
5. **Platform language:** The initial release targets English-speaking users; multi-language support may be added in subsequent iterations.
6. **Notification delivery:** Push notifications are the primary delivery method for recommendations and promotions, as the brief focuses on the mobile application.
