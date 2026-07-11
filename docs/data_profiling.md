# Data Profiling Report

Project: Nova Retail Analytics

Dataset Source:
Brazilian E-Commerce Public Dataset (Olist)

Purpose:
This document summarizes the structure, quality, and characteristics of each dataset before database design and cleaning.

---

# 1. Customers

## Basic Information

| Property | Value |
|----------|--------|
| Table Name | customers |
| Rows | 99,441 |
| Columns | 5 |
| Primary Key Candidate | customer_id |
| Foreign Keys | None |

---

## Columns

| Column | Description |
|---------|-------------|
| customer_id | Unique identifier for each customer account |
| customer_unique_id | Unique identifier for the actual customer |
| customer_zip_code_prefix | Customer ZIP code prefix |
| customer_city | Customer city |
| customer_state | Customer state |

---

## Data Quality Observations

✔ No duplicate customer_id detected (To be verified later using SQL)

✔ No major missing values observed

✔ customer_unique_id may repeat because one customer can have multiple accounts

---

## Business Importance

This table stores customer information and will be used for:

- Customer segmentation
- Regional analysis
- Repeat customer analysis
- Customer Lifetime Value (CLV)

---

# 2. Orders

## Basic Information

| Property | Value |
|----------|--------|
| Rows | 99,442 |
| Columns | 8 |
| Primary Key Candidate | order_id |
| Foreign Key | customer_id |

---

## Data Quality Observations

✔ Missing values found in:

- order_approved_at
- order_delivered_carrier_date
- order_delivered_customer_date

Possible Reason:

Cancelled or unavailable orders.

(To be verified later.)

---

## Business Importance

This is the central transaction table.

It connects customers with products, payments, and reviews.

---

# 3. Order Items

## Basic Information

Rows:
112,650

Columns:
7

Primary Key Candidate:
(order_id + order_item_id)

Foreign Keys:

order_id

product_id

seller_id

---

## Data Quality Observations

Order IDs are repeated because one order can contain multiple products.

This table will become the primary Fact Table.

---

# 4. Products

## Basic Information

| Property | Value |
|----------|--------|
| Table Name | products |
| Rows | 32,951 (or 32,952 depending on dataset version) |
| Columns | 9 |
| Primary Key Candidate | product_id |
| Foreign Keys | product_category_name → category_translation.product_category_name |

---

## Columns

| Column | Description |
|---------|-------------|
| product_id | Unique identifier for each product |
| product_category_name | Product category in Portuguese |
| product_name_lenght | Length of the product name (characters) |
| product_description_lenght | Length of the product description |
| product_photos_qty | Number of product images |
| product_weight_g | Product weight in grams |
| product_length_cm | Product length (cm) |
| product_height_cm | Product height (cm) |
| product_width_cm | Product width (cm) |

---

## Data Quality Observations

✔ Missing values observed in:
- product_category_name
- product_name_lenght
- product_description_lenght
- product_photos_qty

✔ Product dimensions and weight appear to be numeric.

✔ Product category names will require translation using the Category Translation table.

✔ Missing values will be assessed during the data cleaning phase.

---

## Business Importance

This table contains product attributes used for:

- Product performance analysis
- Category analysis
- Logistics analysis
- Product catalog reporting

---

# 5. Order Payments

## Basic Information

| Property | Value |
|----------|--------|
| Table Name | order_payments |
| Rows | 103,886 (or 103,885 depending on dataset version) |
| Columns | 5 |
| Primary Key Candidate | (order_id + payment_sequential) *(To be verified)* |
| Foreign Key | order_id |

---

## Columns

| Column | Description |
|---------|-------------|
| order_id | Order identifier |
| payment_sequential | Sequence number of payment transactions |
| payment_type | Payment method used |
| payment_installments | Number of installments |
| payment_value | Amount paid |

---

## Data Quality Observations

✔ Payment type contains "not_defined" values.

✔ An order may contain multiple payment records.

✔ Payment values should be validated for negative or zero amounts.

✔ Composite key uniqueness will be verified using SQL.

---

## Business Importance

This table supports:

- Revenue analysis
- Payment method analysis
- Installment analysis
- Financial reporting

---

# 6. Sellers

## Basic Information

| Property | Value |
|----------|--------|
| Table Name | sellers |
| Rows | 3,095 (or 3,096 depending on dataset version) |
| Columns | 4 |
| Primary Key Candidate | seller_id |
| Foreign Keys | None |

---

## Columns

| Column | Description |
|---------|-------------|
| seller_id | Unique seller identifier |
| seller_zip_code_prefix | Seller ZIP code prefix |
| seller_city | Seller city |
| seller_state | Seller state |

---

## Data Quality Observations

✔ No major missing values observed during initial inspection.

✔ Seller locations will support regional performance analysis.

✔ Duplicate seller IDs will be verified using SQL.

---

## Business Importance

This table will be used for:

- Seller performance analysis
- Regional seller analysis
- Marketplace insights

---

# 7. Reviews

## Basic Information

| Property | Value |
|----------|--------|
| Table Name | order_reviews |
| Rows | 99,224 (or 99,225 depending on dataset version) |
| Columns | 7 |
| Primary Key Candidate | review_id *(To be verified)* |
| Foreign Key | order_id |

---

## Columns

| Column | Description |
|---------|-------------|
| review_id | Review identifier |
| order_id | Order identifier |
| review_score | Customer rating (1–5) |
| review_comment_title | Review title |
| review_comment_message | Review description |
| review_creation_date | Review creation date |
| review_answer_timestamp | Review response timestamp |

---

## Data Quality Observations

✔ Missing values observed in:
- review_comment_title
- review_comment_message

✔ Many customers submitted ratings without written comments.

✔ Review uniqueness will be validated using SQL profiling.

---

## Business Importance

This table supports:

- Customer satisfaction analysis
- Product quality analysis
- Service quality analysis
- Review score reporting

---

# 8. Category Translation

## Basic Information

| Property | Value |
|----------|--------|
| Table Name | category_translation |
| Rows | 71 (or 72 depending on dataset version) |
| Columns | 2 |
| Primary Key Candidate | product_category_name |
| Foreign Keys | None |

---

## Columns

| Column | Description |
|---------|-------------|
| product_category_name | Product category in Portuguese |
| product_category_name_english | Product category translated into English |

---

## Data Quality Observations

✔ Small lookup table.

✔ Used to translate product categories for reporting.

✔ Duplicate category names will be verified using SQL.

---

## Business Importance

Supports:

- English dashboards
- Product category reporting
- International documentation

---

# 9. Geolocation

## Basic Information

| Property | Value |
|----------|--------|
| Table Name | geolocation |
| Rows | 1,000,163 (or 1,000,164 depending on dataset version) |
| Columns | 5 |
| Primary Key Candidate | None |
| Foreign Keys | None |

---

## Columns

| Column | Description |
|---------|-------------|
| geolocation_zip_code_prefix | ZIP code prefix |
| geolocation_lat | Latitude |
| geolocation_lng | Longitude |
| geolocation_city | City |
| geolocation_state | State |

---

## Data Quality Observations

✔ Multiple records exist for the same ZIP code prefix.

✔ ZIP code prefixes are not unique.

✔ Large dataset intended for geographic analysis.

✔ This table will not be used during the initial database implementation.

---

## Business Importance

Future use cases include:

- Regional mapping
- Delivery analysis
- Logistics optimization
- Geographic visualizations

---
