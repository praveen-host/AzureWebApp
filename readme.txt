 CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    password VARCHAR(100),
    role VARCHAR(50)
);

CREATE TABLE Categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    description TEXT
);

CREATE TABLE Products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    description TEXT,
    category_id INT,
    price DECIMAL(10, 2),
    sku VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES Categories(id)
);

CREATE TABLE Suppliers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    contact_name VARCHAR(100),
    phone VARCHAR(20),
    email VARCHAR(100),
    address VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(100),
    zip_code VARCHAR(20),
    country VARCHAR(100)
);

CREATE TABLE Inventory (
    id SERIAL PRIMARY KEY,
    product_id INT,
    quantity INT,
    location VARCHAR(100),
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES Products(id)
);

CREATE TABLE StockJournal (
    id SERIAL PRIMARY KEY,
    product_id INT,
    quantity_change INT,
    change_type VARCHAR(50),
    reason TEXT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INT,
    FOREIGN KEY (product_id) REFERENCES Products(id),
    FOREIGN KEY (user_id) REFERENCES Users(id)
);

CREATE TABLE PurchaseOrders (
    id SERIAL PRIMARY KEY,
    supplier_id INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(50),
    total_amount DECIMAL(10, 2),
    FOREIGN KEY (supplier_id) REFERENCES Suppliers(id)
);

CREATE TABLE PurchaseOrderItems (
    id SERIAL PRIMARY KEY,
    purchase_order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10, 2),
    total DECIMAL(10, 2),
    FOREIGN KEY (purchase_order_id) REFERENCES PurchaseOrders(id),
    FOREIGN KEY (product_id) REFERENCES Products(id)
);

CREATE TABLE Customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    address VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(100),
    zip_code VARCHAR(20),
    country VARCHAR(100)
);

CREATE TABLE SalesOrders (
    id SERIAL PRIMARY KEY,
    customer_id INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(50),
    total_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES Customers(id)
);

CREATE TABLE SalesOrderItems (
    id SERIAL PRIMARY KEY,
    sales_order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10, 2),
    total DECIMAL(10, 2),
    FOREIGN KEY (sales_order_id) REFERENCES SalesOrders(id),
    FOREIGN KEY (product_id) REFERENCES Products(id)
);




<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>New Item Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .container {
            width: 80%;
            margin: 0 auto;
        }
        .form-group {
            margin-bottom: 1em;
        }
        .form-group label {
            display: block;
            margin-bottom: 0.5em;
        }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 0.5em;
            box-sizing: border-box;
        }
        .form-group input[type="checkbox"] {
            width: auto;
        }
        .image-upload {
            border: 1px dashed #ccc;
            padding: 1em;
            text-align: center;
        }
        .image-upload p {
            margin: 0;
        }
        .form-actions {
            margin-top: 1em;
            text-align: right;
        }
        .form-actions button {
            padding: 0.5em 1em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>New Item</h1>
        <form>
            <div class="form-group">
                <label>Type</label>
                <input type="radio" name="type" value="goods" checked> Goods
                <input type="radio" name="type" value="service"> Service
            </div>
            <div class="form-group">
                <label for="name">Name*</label>
                <input type="text" id="name" name="name" required>
            </div>
            <div class="form-group">
                <label for="sku">SKU</label>
                <input type="text" id="sku" name="sku">
            </div>
            <div class="form-group">
                <label for="unit">Unit*</label>
                <select id="unit" name="unit" required>
                    <option value="">Select or type to add</option>
                </select>
            </div>
            <div class="form-group">
                <input type="checkbox" id="returnable" name="returnable">
                <label for="returnable">Returnable Item</label>
            </div>
            <div class="form-group">
                <label for="dimensions">Dimensions (Length x Width x Height)</label>
                <input type="text" id="dimensions" name="dimensions">
            </div>
            <div class="form-group">
                <label for="weight">Weight</label>
                <input type="text" id="weight" name="weight">
                <select name="weight_unit">
                    <option value="kg">kg</option>
                    <option value="g">g</option>
                    <option value="lb">lb</option>
                    <option value="oz">oz</option>
                </select>
            </div>
            <div class="form-group">
                <label for="manufacturer">Manufacturer</label>
                <select id="manufacturer" name="manufacturer">
                    <option value="">Select or Add Manufacturer</option>
                </select>
            </div>
            <div class="form-group">
                <label for="brand">Brand</label>
                <select id="brand" name="brand">
                    <option value="">Select or Add Brand</option>
                </select>
            </div>
            <div class="form-group">
                <label for="upc">UPC</label>
                <input type="text" id="upc" name="upc">
            </div>
            <div class="form-group image-upload">
                <label>Images</label>
                <div>
                    <p>Drag image(s) here or</p>
                    <button type="button">Browse images</button>
                    <p>You can add up to 15 images, each not exceeding 5 MB.</p>
                </div>
            </div>
            <div class="form-actions">
                <button type="submit">Save</button>
                <button type="button">Cancel</button>
            </div>
        </form>
    </div>
</body>
</html>
