Sprint 1: System Architecture & Scope Definition
Section 1: Target Audience & Market Focus
Primary Persona: Independent artisans and small business owners (ages 25–45) who handcraft goods (jewelry, home décor, apparel) and need an affordable, easy-to-manage online storefront without the overhead of enterprise e-commerce platforms.
Core Pain Point: Existing platforms are either too expensive (high transaction fees, monthly subscriptions) or too complex to set up and maintain for a solo seller or small team, making it hard to manage inventory, orders, and payments in one place.
Domain Scope: Handmade & Artisan Goods (a sub-vertical of Consumer Retail/Apparel).
Section 2: MVP Feature Scope
Category
Feature Name
Description
Priority
Authentication
User Registration & Authentication
Password hashing (bcrypt) and JWT-based session/authentication mechanism for buyers and sellers.
High (MVP)
Catalog
Product List & Search
Product browsing interface with category-based filtering and keyword search.
High (MVP)
Cart
Cart Management
State-persistent cart management supporting item addition, quantity update, and removal.
High (MVP)
Checkout
Order Processing
Stripe (test mode) payment gateway integration and order object instantiation on successful payment.
High (MVP)
Admin
Inventory Control
Administrative CRUD operations for product listings and stock levels.
Medium
Account
Order History
Buyers can view past orders and current order status.
Medium
Section 3: Tech Stack Selection & Justification
Frontend Framework: React (with Vite)
Justification: React's component model fits a catalog/cart UI with frequently changing state (cart contents, filters). Vite gives fast local iteration compared to older bundlers, and the team already has React experience, reducing ramp-up time.
Backend Infrastructure: Node.js / Express
Justification: Express is lightweight and unopinionated, letting the team define REST routes for auth, catalog, cart, and orders quickly. Using JavaScript across frontend and backend reduces context-switching for a small student team, compared to introducing a second language like Python (Django) or Java (Spring Boot).
Database Management System: PostgreSQL
Justification: The domain is inherently relational (users → orders → order items → products → categories) with strict referential integrity needs (e.g., an order item must reference a valid product and order). PostgreSQL's foreign key constraints and transactional guarantees are a better fit than a document store like MongoDB for this schema.
Caching & Asynchronous Processing (Optional): Redis
Justification: Redis can store session/cart data for guest users and cache frequently-read product listings, reducing repeated database hits during peak browsing.
Section 4: Entity-Relationship Diagram (ERD)
Mermaid
Relationship & Cardinality Notes:
USERS 1:N ORDERS — a user can place many orders; each order belongs to one user.
USERS 1:1 CART — each user has exactly one active cart.
ORDERS 1:N ORDER_ITEMS — an order contains one or more line items.
PRODUCTS 1:N ORDER_ITEMS — a product can appear in many order line items.
CATEGORIES 1:N PRODUCTS — a category groups many products; each product belongs to one category.
CART 1:N CART_ITEMS — a cart holds one or more cart line items.
PRODUCTS 1:N CART_ITEMS — a product can be present in many users' carts.
ORDER_ITEMS and CART_ITEMS are associative entities resolving the N:M relationships between orders/carts and products.
