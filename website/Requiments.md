# Software Requirements Specification (SRS)
**Project Title:** E-Commerce Perfume Store (WhatsApp Checkout & Local Wishlist)  
**Document Version:** 1.0 (Final Specifications)  
**Target Platform:** Web Application (Mobile-First / Responsive)

---

## 1. Executive Summary
The goal of this project is to develop a highly responsive, single-page e-commerce web application for a boutique perfume brand. The store prioritizes a seamless, high-speed mobile shopping experience: customers can explore catalog products, filter by scent profiles, customize sizes and gift packaging, manage a client-side Wishlist, and complete orders directly via WhatsApp—without the barrier of account creation or complex payment gateways.

---

## 2. User Roles & Access Control
- **Guest Visitor:** Browses product catalog, applies filters/sorting, views product detail pages (PDP), manages local Wishlist, selects product variants and gift options, submits guest checkout (routed to WhatsApp), submits customer reviews, and sends contact inquiries.
- **Store Admin (Single Owner):** Authenticated store owner with full administrative access to manage product inventory, toggle availability, manage contact inquiries, moderate customer reviews, and update FAQ content.

---

## 3. Functional Requirements (FR)

### 3.1 Product Catalog & Navigation
- **FR-01 (Single Catalog Landing):** The system shall load all primary products directly on the main page without requiring an extra landing page.
- **FR-02 (Catalog Navigation & PDP):** Clicking any product card within the main catalog grid shall navigate the user to a dedicated Product Detail Page (PDP) displaying full product details, multi-angle images, size options, gift customization, and approved customer reviews.
- **FR-03 (Instant Search):** The system shall provide a real-time search input that filters catalog products dynamically by name/title as the user types.
- **FR-04 (Multi-Attribute Filtering):** Users shall be able to filter products by:
  - Price range (via a dynamic slider/range filter).
  - Occasion (e.g., Daily, Formal, Evening).
  - Fragrance Profile / Scent Family (e.g., Woody, Floral, Citrus, Oriental).
- **FR-05 (Catalog Sorting):** The catalog shall provide a sorting interface supporting:
  - **Default Sort:** Newest Arrivals (ordered by latest creation timestamp).
  - Price: Low to High.
  - Price: High to Low.

### 3.2 Product Variants, Packaging & Stock Logic
- **FR-06 (Size Variants & Default Pricing):** Products shall support size variants (e.g., 50ml, 100ml) with independent pricing. By default, catalog cards and PDPs shall display the smallest size variant and its corresponding price.
- **FR-07 (Gift Wrapping Option):** Each product shall include a gift wrapping option toggle with a fixed extra fee displayed on the product view. Selecting gift wrapping shall reveal an optional custom text field for gift notes.
- **FR-08 (Out-of-Stock Handling):**
  - Products marked as `Out of Stock` shall remain visible in the catalog with an "Out of Stock" (غير متوفر حالياً) badge, but adding them to the cart shall be disabled.
  - Complete removal of a product from the site shall only occur through manual deletion by the Admin.
  - Exact inventory counts (e.g., "3 left in stock") shall **not** be exposed to end users.

### 3.3 Client-Side Wishlist
- **FR-09 (Local Wishlist Operations):** Users can add products to or remove them from a Wishlist without creating an account.
- **FR-10 (Client-Side Persistence):** Wishlist state shall persist locally on the user's browser/device (using Web Storage like `localStorage`) to remain saved across future visits from the same device.

### 3.4 Shopping Cart & WhatsApp Checkout
- **FR-11 (Cart Management):** Users can add items, select specific sizes, enable gift wrapping (with custom notes), and adjust quantities inside a guest cart drawer/page.
- **FR-12 (Guest Checkout Form):** Checkout requires zero registration. Customers submit minimal required delivery details:
  - Full Name
  - Contact Phone Number
  - Detailed Shipping Address
- **FR-13 (WhatsApp Order Dispatch):** Submitting checkout compiles an order payload and opens WhatsApp (App/Web) directed to the owner's WhatsApp number with a structured message containing:
  - Itemized product list (Selected sizes, quantities, gift wrapping options, and gift notes)
  - Calculated total order amount
  - Customer contact and delivery details

### 3.5 Reviews & Inquiries
- **FR-14 (Review Submission):** Customers can submit star ratings and written reviews on product detail pages.
- **FR-15 (Review Moderation Workflow):** Submitted reviews default to a `Pending` state and shall **not** appear publicly until explicitly approved by the Store Admin.
- **FR-16 (FAQ Page):** A dedicated page displaying categorized questions and answers.
- **FR-17 (Contact Us Form):** A page displaying store contact info (phone/email) and a quick contact form (Name, Contact Info, Message).

### 3.6 Admin Dashboard
- **FR-18 (Single Admin Authentication):** Secure login interface restricted strictly to the single store owner.
- **FR-19 (Product CRUD & Stock Toggle):** The Admin shall be able to create, edit, delete, and manually switch product status between `Available` and `Out of Stock`.
- **FR-20 (Inquiry Management):** A dedicated panel to read, manage, and clear messages submitted through the Contact Us form.
- **FR-21 (Review Moderation Panel):** Panel to inspect pending reviews and trigger `Approve` or `Reject` actions.
- **FR-22 (FAQ Content Management):** Interface to add, edit, or remove FAQ items.
- **FR-23 (No Order Data Storage):** Orders shall **not** be saved or managed in the Admin Dashboard database, as all order transactions are handled natively via WhatsApp chats.

---

## 4. Non-Functional Requirements (NFR)

### 4.1 Mobile Optimization & UX
- **NFR-01 (Mobile-First Experience):** The user interface must be engineered using a Mobile-First approach. All interactions (filter drawers, touch targets, wishlist toggles, WhatsApp handoff) must be optimized for thumb interaction on small touchscreens.

### 4.2 Performance & Low-Bandwidth Efficiency
- **NFR-02 (Media Compression):** Product images must be automatically compressed and served in lightweight WebP/AVIF formats.
- **NFR-03 (Lazy Loading):** Images and off-screen assets must use lazy loading to render content only as it enters the user's viewport.
- **NFR-04 (Page Load Metrics):** First Contentful Paint (FCP) must execute in under 1.2 seconds and Largest Contentful Paint (LCP) under 2.0 seconds on standard 3G/4G connections.

### 4.3 Security & Integrity
- **NFR-05 (Admin Security):** Admin authentication must use secure session handling (HTTP-only cookies or JWT) to protect dashboard routes and contact submissions.
- **NFR-06 (Anti-Spam Controls):** Public forms (Contact Form and Reviews) must implement anti-spam measures (e.g., Rate Limiting / Honeypot fields).











---
-----
---
---
---
---
---
--
