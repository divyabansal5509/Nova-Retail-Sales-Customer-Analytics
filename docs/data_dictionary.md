# Data Dictionary

## Project
Nova Retail – Sales & Customer Analytics

## Purpose
This document describes the structure and meaning of every column used in the Nova Retail Analytics project. It serves as a reference for database design, SQL analysis, Power BI dashboards, and project documentation.

---

# 1. Customers

| Column | Data Type | Description |
|---------|-----------|-------------|
| customer_id | VARCHAR | Unique identifier for each customer account |
| customer_unique_id | VARCHAR | Unique identifier representing an individual customer across multiple accounts |
| customer_zip_code_prefix | INTEGER | ZIP code prefix of the customer's location |
| customer_city | VARCHAR | Customer's city |
| customer_state | VARCHAR | Customer's state |

# 2. Orders

| Column | Data Type | Description |
|---------|-----------|-------------|
| order_id | VARCHAR | Unique identifier for each order |
| customer_id | VARCHAR | Customer who placed the order |
| order_status | VARCHAR | Current order status (delivered, shipped, canceled, etc.) |
| order_purchase_timestamp | TIMESTAMP | Date and time when the order was placed |
| order_approved_at | TIMESTAMP | Date and time when the payment was approved |
| order_delivered_carrier_date | TIMESTAMP | Date and time when the carrier received the package |
| order_delivered_customer_date | TIMESTAMP | Date and time when the customer received the order |
| order_estimated_delivery_date | TIMESTAMP | Estimated delivery date provided to the customer |

# 3. Order Items

| Column | Data Type | Description |
|---------|-----------|-------------|
| order_id | VARCHAR | Order identifier |
| order_item_id | INTEGER | Sequential item number within an order |
| product_id | VARCHAR | Product identifier |
| seller_id | VARCHAR | Seller responsible for the product |
| shipping_limit_date | TIMESTAMP | Shipping deadline for the seller |
| price | DECIMAL | Price of the product |
| freight_value | DECIMAL | Shipping cost charged for the item |

# 4. Products

| Column | Data Type | Description |
|---------|-----------|-------------|
| product_id | VARCHAR | Unique identifier for each product |
| product_category_name | VARCHAR | Product category in Portuguese |
| product_name_lenght | INTEGER | Number of characters in the product name |
| product_description_lenght | INTEGER | Number of characters in the product description |
| product_photos_qty | INTEGER | Number of product images |
| product_weight_g | DECIMAL | Product weight in grams |
| product_length_cm | DECIMAL | Product length in centimeters |
| product_height_cm | DECIMAL | Product height in centimeters |
| product_width_cm | DECIMAL | Product width in centimeters |

# 5. Order Payments

| Column | Data Type | Description |
|---------|-----------|-------------|
| order_id | VARCHAR | Order identifier |
| payment_sequential | INTEGER | Sequence number of the payment transaction |
| payment_type | VARCHAR | Payment method used by the customer |
| payment_installments | INTEGER | Number of payment installments |
| payment_value | DECIMAL | Total payment amount |

# 6. Sellers

| Column | Data Type | Description |
|---------|-----------|-------------|
| seller_id | VARCHAR | Unique identifier for each seller |
| seller_zip_code_prefix | INTEGER | Seller ZIP code prefix |
| seller_city | VARCHAR | Seller city |
| seller_state | VARCHAR | Seller state |

# 7. Reviews

| Column | Data Type | Description |
|---------|-----------|-------------|
| review_id | VARCHAR | Review identifier |
| order_id | VARCHAR | Order identifier associated with the review |
| review_score | INTEGER | Customer rating from 1 to 5 |
| review_comment_title | VARCHAR | Title of the customer review |
| review_comment_message | TEXT | Customer review comment |
| review_creation_date | DATE | Date the review was created |
| review_answer_timestamp | TIMESTAMP | Date and time when the review was processed |

# 8. Category Translation

| Column | Data Type | Description |
|---------|-----------|-------------|
| product_category_name | VARCHAR | Product category name in Portuguese |
| product_category_name_english | VARCHAR | English translation of the product category |

# 9. Geolocation

| Column | Data Type | Description |
|---------|-----------|-------------|
| geolocation_zip_code_prefix | INTEGER | ZIP code prefix |
| geolocation_lat | DECIMAL | Latitude coordinate |
| geolocation_lng | DECIMAL | Longitude coordinate |
| geolocation_city | VARCHAR | City name |
| geolocation_state | VARCHAR | State abbreviation |

