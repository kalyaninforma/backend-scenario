# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a REST API for an e-commerce application built with Node.js and Express. The project is currently in the initial setup phase with requirements documented but no implementation yet.

## Database Schema

The database schema is defined in `docs/database-schema.png` and includes the following main entities:

- **customers**: Customer information (customer_id, customer_unique_id, customer_zip_code_prefix, customer_city, customer_state)
- **orders**: Order records with status tracking, timestamps for purchase/approval/delivery dates
- **order_items**: Individual items within orders, linked to products and sellers with pricing and shipping details
- **order_payments**: Payment information including type, installments, and values
- **order_reviews**: Customer reviews with scores and comments
- **products**: Product catalog with category, dimensions, weight, and photo quantity
- **product_category_name_translation**: Category name translations
- **sellers**: Seller information with location details
- **geolocation**: Geographic data with zip codes, coordinates, and location details
- **leads_qualified**: Marketing qualified leads with contact and origin information
- **leads_closed**: Closed leads with sales representative and business details

Key relationships:
- Orders belong to customers (customers.customer_id → orders.customer_id)
- Order items belong to orders (orders.order_id → order_items.order_id)
- Order items reference products (products.product_id → order_items.product_id)
- Order items reference sellers (sellers.seller_id → order_items.seller_id)
- Order payments link to orders (orders.order_id → order_payments.order_id)
- Order reviews link to orders (orders.order_id → order_reviews.order_id)

## Required API Endpoints

See `docs/requirements.md` for detailed specifications. The core endpoints to implement:

1. **GET /products** - List all available products with ID, name, price, and stock
2. **POST /customers** - Register a new customer with unique ID, zip code, city, and state
3. **POST /orders** - Create an order with customer ID, product items (ID, quantity, price), and status
4. **GET /customers/{customer_id}/orders** - View a customer's order history with full details

## Technology Stack

- **Backend Framework**: Node.js with Express
- **Database**: To be determined (schema provided suggests relational DB like PostgreSQL or MySQL)

## Development Workflow

When implementing this project:

1. Set up Node.js/Express project structure with package.json
2. Choose and configure database (PostgreSQL/MySQL recommended based on schema complexity)
3. Implement database migrations/schema based on the provided database schema diagram
4. Create data models/entities matching the schema
5. Implement route handlers for each required endpoint
6. Add input validation and error handling
7. Test endpoints against the expected inputs/outputs in requirements.md

## Important Considerations

- The database schema includes many tables beyond the minimum requirements (sellers, reviews, payments, leads), suggesting the API may need to expand beyond the initial 4 endpoints
- Pay attention to relationships between tables when implementing business logic
- Order creation should handle multiple order_items and validate product availability
- Customer registration uses both customer_id and customer_unique_id - understand the distinction
