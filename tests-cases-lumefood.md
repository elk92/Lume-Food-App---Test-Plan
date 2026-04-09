# 10. Functional Test Scenarios (User Flows)

## 10.1 Test Data

### Customer Users
| Email | Password | Name |
|------|----------|------|
| joao@lumefood.com | senha123 | João Silva |
| maria@lumefood.com | senha123 | Maria Santos |
| pedro@lumefood.com | senha123 | Pedro Oliveira |

### Admin Users
| Email | Password | Restaurant |
|------|----------|------------|
| admin.pizzaria@lumefood.com | admin123 | Pizzaria do Chef |
| admin.burguer@lumefood.com | admin123 | Burguer King Premium |

### Coupon
- Code: **LUMEFOOD10** (10% discount)

---

## 10.2 Critical User Flows

### 📌 FT01 – Customer Login

| ID   | Scenario |
|------|---------|
| FT01 | Login with valid credentials |

**Steps:**
- Access `/login`
- Enter valid credentials (joao@lumefood.com / senha123)
- Submit form

**Expected Result:**
- User is authenticated
- Redirected to home page

---

### 📌 FT02 – Browse Restaurants

| ID   | Scenario |
|------|---------|
| FT02 | View restaurant list |

**Steps:**
- Access `/restaurantes`
- View available restaurants

**Expected Result:**
- Restaurants are listed correctly
- Data matches API response

---

### 📌 FT03 – View Restaurant Menu

| ID   | Scenario |
|------|---------|
| FT03 | Access restaurant details |

**Steps:**
- Click on a restaurant
- Navigate to `/restaurante/:id`

**Expected Result:**
- Menu is displayed with categories
- Products are visible

---

### 📌 FT04 – Add Item to Cart

| ID   | Scenario |
|------|---------|
| FT04 | Add product to cart |

**Steps:**
- Access `/restaurantes`
- Select restaurant
- Click "Adicionar"

**Expected Result:**
- Item is added successfully
- Cart updates correctly

---

### 📌 FT05 – Update Cart

| ID   | Scenario |
|------|---------|
| FT05 | Update item quantity |

**Steps:**
- Access `/carrinho`
- Increase/decrease quantity

**Expected Result:**
- Values updated correctly
- Total recalculated

---

### 📌 FT06 – Apply Coupon

| ID   | Scenario |
|------|---------|
| FT06 | Apply discount coupon |

**Steps:**
- Go to `/checkout`
- Apply coupon `LUMEFOOD10`

**Expected Result:**
- 10% discount applied
- Total updated

---

### 📌 FT07 – Checkout Flow

| ID   | Scenario |
|------|---------|
| FT07 | Complete order |

**Steps:**
- Proceed to `/checkout`
- Fill required fields
- Confirm order

**Expected Result:**
- Order created successfully
- Redirect to `/pedidos`

---

### 📌 FT08 – View Orders

| ID   | Scenario |
|------|---------|
| FT08 | View order history |

**Steps:**
- Access `/pedidos`

**Expected Result:**
- Orders listed correctly

---

### 📌 FT09 – Admin Manage Menu

| ID   | Scenario |
|------|---------|
| FT09 | Admin creates menu item |

**Steps:**
- Login as admin
- Access `/admin/cardapio`
- Create new item

**Expected Result:**
- Item appears in menu

---

### 📌 FT10 – Admin Manage Orders

| ID   | Scenario |
|------|---------|
| FT10 | Update order status |

**Steps:**
- Access `/admin/pedidos`
- Change order status

**Expected Result:**
- Status updated successfully

---

## 11. API Test Scenarios

---

## 11.1 Authentication

### 📌 API01 – Register User (Positive)

- POST `/api/register`

**Steps:**
- Send valid payload (email, password)

**Validations:**
- Status 201
- User created successfully
- Response contains user ID

---

### 📌 API01-N – Register User (Negative)

**Steps:**
- Send request with missing fields (email or password)
- Send invalid email format

**Validations:**
- Status 400
- Proper error message returned

---

### 📌 API01-C – Contract Validation

**Validations:**
- Response schema contains:
  - id (string/number)
  - email (string)
- No unexpected fields
- Data types are correct

---

## 11.2 Restaurants

### 📌 API02 – Get Restaurants (Positive)

- GET `/api/restaurantes`

**Steps:**
- Send request without authentication

**Validations:**
- Status 200
- Response is an array
- List is not empty

---

### 📌 API02-N – Get Restaurants (Negative)

**Steps:**
- Simulate server failure or invalid route

**Validations:**
- Status 4xx or 5xx
- Proper error handling

---

### 📌 API02-C – Contract Validation

**Validations:**
- Each item contains:
  - id
  - name
  - description
- Data types are consistent

---

### 📌 API03 – Get Restaurant Details (Positive)

- GET `/api/restaurantes/:id`

**Steps:**
- Send valid restaurant ID

**Validations:**
- Status 200
- Includes menu data

---

### 📌 API03-N – Get Restaurant Details (Negative)

**Steps:**
- Send invalid/non-existing ID

**Validations:**
- Status 404
- Error message returned

---

### 📌 API03-C – Contract Validation

**Validations:**
- Response contains:
  - restaurant info
  - menu array
- Proper schema structure

---

## 11.3 Cart

### 📌 API04 – Add Item to Cart (Positive)

- POST `/api/carrinho/items`

**Steps:**
- Send valid product ID and quantity

**Validations:**
- Status 200
- Item added

---

### 📌 API04-N – Add Item to Cart (Negative)

**Steps:**
- Send invalid product ID
- Send quantity = 0 or negative

**Validations:**
- Status 400
- Error message returned

---

### 📌 API04-C – Contract Validation

**Validations:**
- Response contains:
  - itemId
  - quantity
- Correct data types

---

### 📌 API05 – Update Cart Item

- PATCH `/api/carrinho/items/:id`

**Steps:**
- Update quantity

**Validations:**
- Quantity updated correctly

---

### 📌 API05-N – Update Cart Item (Negative)

**Steps:**
- Update with invalid ID

**Validations:**
- Status 404

---

### 📌 API06 – Remove Item

- DELETE `/api/carrinho/items/:id`

**Validations:**
- Item removed

---

### 📌 API06-N – Remove Item (Negative)

**Steps:**
- Remove non-existing item

**Validations:**
- Status 404

---

## 11.4 Orders

### 📌 API07 – Create Order (Positive)

- POST `/api/pedidos`

**Steps:**
- Send valid cart data

**Validations:**
- Status 201
- Order created

---

### 📌 API07-N – Create Order (Negative)

**Steps:**
- Send empty cart
- Send invalid data

**Validations:**
- Status 400
- Order not created

---

### 📌 API07-C – Contract Validation

**Validations:**
- Response contains:
  - orderId
  - total
  - status
- Correct types

---

### 📌 API08 – Get Orders

- GET `/api/pedidos`

**Validations:**
- Returns list of orders

---

### 📌 API08-N – Get Orders (Unauthorized)

**Steps:**
- Call endpoint without authentication

**Validations:**
- Status 401

---

### 📌 API09 – Order Details

- GET `/api/pedidos/:id`

**Validations:**
- Correct order data

---

### 📌 API09-N – Order Details (Invalid ID)

**Steps:**
- Send invalid ID

**Validations:**
- Status 404

---

## 11.5 Coupon

### 📌 API10 – Validate Coupon (Positive)

- POST `/api/cupons/validar`

**Steps:**
- Send coupon `LUMEFOOD10`

**Validations:**
- Discount applied (10%)

---

### 📌 API10-N – Validate Coupon (Negative)

**Steps:**
- Send invalid coupon

**Validations:**
- Status 400
- Error message returned

---

### 📌 API10-C – Contract Validation

**Validations:**
- Response contains:
  - valid (boolean)
  - discount (number)

---

## 11.6 Admin APIs

### 📌 API11 – Admin Menu Management

**Positive:**
- Create, update, delete items

**Negative:**
- Non-admin user attempts access → 403

**Contract:**
- Validate item schema

---

### 📌 API12 – Admin Orders

- GET `/api/admin/pedidos`

**Negative:**
- Unauthorized access → 401/403

---

### 📌 API13 – Update Order Status

- PATCH `/api/pedidos/:id/status`

**Steps:**
- Update order status

**Validations:**
- Status updated correctly

---

### 📌 API13-N – Update Order Status (Invalid)

**Steps:**
- Send invalid status

**Validations:**
- Status 400

---

## 12. Edge Cases (Functional)

---

### 📌 EC01 – Checkout with Empty Cart

**Steps:**
- Access `/carrinho`
- Ensure cart is empty
- Attempt to proceed to `/checkout`

**Expected Result:**
- Checkout blocked
- Error message displayed

---

### 📌 EC02 – Invalid Coupon

**Steps:**
- Add item to cart
- Go to `/checkout`
- Apply invalid coupon

**Expected Result:**
- Coupon rejected
- Proper error message

---

### 📌 EC03 – Unauthorized Admin Access

**Steps:**
- Login as customer
- Access `/admin`

**Expected Result:**
- Access denied
- Redirect or error

---

### 📌 EC04 – Duplicate Order Submission

**Steps:**
- Complete checkout
- Click confirm multiple times

**Expected Result:**
- Only one order created

---

### 📌 EC05 – Invalid Login

**Steps:**
- Enter wrong credentials

**Expected Result:**
- Login fails
- Error message displayed

---

### 📌 EC06 – Expired Session

**Steps:**
- Login
- Simulate session expiration
- Perform action

**Expected Result:**
- User redirected to login
