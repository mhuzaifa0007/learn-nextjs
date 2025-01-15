# Data Schema for Artisan Goods Marketplace

## 1. Users Table
This table stores both buyers and sellers. The `role` attribute determines the type of user.

### Attributes:
- **user_id** (Primary Key) - Unique identifier for each user.
- **name** (String) - Full name of the user.
- **email** (String, Unique) - Email address of the user.
- **password** (String) - Hashed password for authentication.
- **address** (Text) - Shipping and billing address.
- **role** (Enum: 'buyer', 'seller', 'admin') - Defines the user’s role in the marketplace.
- **phone_number** (String, Nullable) - User’s phone number.
- **profile_picture** (String, Nullable) - URL to the user’s profile picture.
- **created_at** (Timestamp) - Account creation date.
- **updated_at** (Timestamp) - Account last updated timestamp.

### Constraints:
- **Unique Index**: `email` for ensuring no duplicate users.

## 2. Products Table
The products table holds all product listings from sellers.

### Attributes:
- **product_id** (Primary Key) - Unique identifier for each product.
- **name** (String) - Product name.
- **description** (Text) - Detailed description of the product.
- **price** (Decimal) - Product price.
- **stock_quantity** (Integer) - Available quantity in stock.
- **category_id** (Foreign Key) - Links to the `categories` table.
- **seller_id** (Foreign Key) - Links to the `users` table (the seller).
- **created_at** (Timestamp) - Date the product was listed.
- **updated_at** (Timestamp) - Date the product was last updated.

### Constraints:
- **Foreign Key**: `category_id` references `categories.category_id`.
- **Foreign Key**: `seller_id` references `users.user_id`.
- **Indexing**: Create indexes on `price`, `category_id`, and `seller_id` for faster search queries.

## 3. Transactions Table
This table tracks completed transactions on the marketplace.

### Attributes:
- **transaction_id** (Primary Key) - Unique transaction identifier.
- **buyer_id** (Foreign Key) - Links to the `users` table (the buyer).
- **product_id** (Foreign Key) - Links to the `products` table (the product purchased).
- **quantity** (Integer) - Quantity of the product purchased.
- **total_price** (Decimal) - Total cost for the transaction.
- **status** (Enum: 'pending', 'completed', 'cancelled') - Status of the transaction.
- **created_at** (Timestamp) - Date the transaction was created.
- **updated_at** (Timestamp) - Date the transaction was last updated.

### Constraints:
- **Foreign Key**: `buyer_id` references `users.user_id`.
- **Foreign Key**: `product_id` references `products.product_id`.

## 4. Categories Table
This table defines product categories for better navigation and organization.

### Attributes:
- **category_id** (Primary Key) - Unique identifier for each category.
- **name** (String) - Name of the category (e.g., Jewelry, Art, Home Decor).
- **description** (Text, Nullable) - Description of the category.
- **created_at** (Timestamp) - Date the category was created.
- **updated_at** (Timestamp) - Date the category was last updated.

## 5. Audit Log Table (Advanced)
This table tracks changes made to critical marketplace entities for security and compliance purposes.

### Attributes:
- **audit_log_id** (Primary Key) - Unique identifier for each log.
- **action** (String) - Description of the action taken (e.g., 'Product Created', 'Transaction Completed').
- **entity_type** (Enum: 'user', 'product', 'transaction') - The type of entity that was affected.
- **entity_id** (Integer) - The ID of the entity that was changed.
- **old_value** (Text) - The previous state of the entity (in JSON format).
- **new_value** (Text) - The new state of the entity (in JSON format).
- **timestamp** (Timestamp) - Date and time of the action.

### Example Relations:
- A **User** can have many **Products** (1-to-many relationship).
- A **Product** can appear in many **Transactions** (many-to-many relationship with `Transactions_Products` join table).
