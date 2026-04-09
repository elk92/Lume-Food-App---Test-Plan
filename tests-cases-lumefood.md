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

## 10.2 Functional Test Scenarios (Extended Coverage)

---

### AUTH – SIGN UP

| ID      | Feature | Scenario                          | Steps                                                                 | Expected Result                      | Severity |
|---------|--------|----------------------------------|-----------------------------------------------------------------------|--------------------------------------|----------|
| FT00    | Auth   | Valid user registration          | Access `/login` → Click "Sign Up" → Fill Name, Email, Password → Submit | User created successfully            | High     |
| FT00-N1 | Auth   | Register with existing email     | Use already registered email                                          | Error message displayed              | High     |
| FT00-N2 | Auth   | Register with invalid email      | Enter invalid email (ex: user@)                                       | Validation error                     | Medium   |
| FT00-N3 | Auth   | Register with empty fields       | Submit without filling fields                                         | Required field validation            | High     |
| FT00-N4 | Auth   | Register with weak password      | Enter short/invalid password                                          | Validation error                     | Medium   |

---

### AUTH – LOGIN

| ID      | Feature | Scenario                      | Steps                                              | Expected Result       | Severity |
|---------|--------|------------------------------|----------------------------------------------------|-----------------------|----------|
| FT01    | Auth   | Login with valid credentials | Access `/login` → Enter valid credentials → Submit | User logged in        | High     |
| FT01-N1 | Auth   | Invalid credentials          | Enter wrong password                               | Error displayed       | High     |
| FT01-N2 | Auth   | Empty fields                 | Submit empty form                                  | Validation errors     | Medium   |
| FT01-N3 | Auth   | Invalid email format         | Enter invalid email                                | Validation error      | Medium   |

---

### CATALOG

| ID      | Feature | Scenario                    | Steps        | Expected Result           | Severity |
|---------|--------|-----------------------------|--------------|----------------------------|----------|
| FT02    | Catalog| View restaurants            | Access `/`   | Restaurants listed         | Medium   |
| FT02-N1 | Catalog| API failure on listing      | Simulate API | Error message shown        | Medium   |

---

### RESTAURANT MENU

| ID      | Feature | Scenario                    | Steps                          | Expected Result     | Severity |
|---------|--------|-----------------------------|--------------------------------|----------------------|----------|
| FT03    | Menu   | View restaurant menu        | Access `/restaurante/:id`      | Menu displayed       | Medium   |
| FT03-N1 | Menu   | Invalid restaurant ID       | Access invalid ID              | Error or redirect    | Medium   |

---

### CART

| ID      | Feature | Scenario                    | Steps                | Expected Result         | Severity |
|---------|--------|-----------------------------|----------------------|--------------------------|----------|
| FT04    | Cart   | Add item to cart            | Select item → Add    | Item added               | High     |
| FT04-N1 | Cart   | Add unavailable product     | Add out-of-stock     | Error displayed          | High     |
| FT05    | Cart   | Update quantity             | Change quantity      | Updated correctly        | High     |
| FT05-N1 | Cart   | Invalid quantity            | Set 0 or negative    | Validation error         | High     |

---

### COUPON

| ID      | Feature  | Scenario                  | Steps                    | Expected Result     | Severity |
|---------|----------|---------------------------|---------------------------|----------------------|----------|
| FT06    | Checkout | Apply valid coupon        | Apply LUMEFOOD10          | Discount applied     | High     |
| FT06-N1 | Checkout | Invalid coupon            | Apply wrong code          | Error message        | Medium   |
| FT06-N2 | Checkout | Expired coupon            | Apply expired code        | Error message        | Medium   |

---

### CHECKOUT

| ID      | Feature  | Scenario                       | Steps                     | Expected Result        | Severity |
|---------|----------|--------------------------------|----------------------------|------------------------|----------|
| FT07    | Checkout | Complete order                 | Fill data → Confirm        | Order created          | High     |
| FT07-N1 | Checkout | Empty cart                    | Proceed empty cart         | Blocked                | High     |
| FT07-N2 | Checkout | Invalid payment               | Enter invalid data         | Error message          | High     |
| FT07-N3 | Checkout | API failure                   | Simulate failure           | Graceful error         | High     |

---

### ORDERS

| ID      | Feature | Scenario            | Steps              | Expected Result     | Severity |
|---------|--------|---------------------|---------------------|----------------------|----------|
| FT08    | Orders | View orders         | Access `/pedidos`   | Orders listed        | Medium   |
| FT08-N1 | Orders | No orders           | New user access     | Empty state shown    | Low      |

---

### ADMIN – MENU

| ID      | Feature | Scenario              | Steps                                | Expected Result   | Severity |
|---------|--------|------------------------|----------------------------------------|--------------------|----------|
| FT09    | Admin  | Create menu item       | `/admin/cardapio` → Create            | Item created       | High     |
| FT09-N1 | Admin  | Invalid item data      | Missing fields                         | Validation error   | Medium   |
| FT09-N2 | Admin  | Unauthorized access    | Non-admin access                       | Access denied      | High     |

---

### ADMIN – ORDERS

| ID      | Feature | Scenario               | Steps                     | Expected Result   | Severity |
|---------|--------|------------------------|----------------------------|--------------------|----------|
| FT10    | Admin  | Update order status    | Change status              | Updated            | High     |
| FT10-N1 | Admin  | Invalid status         | Send invalid status        | Error message      | Medium   |
| FT10-N2 | Admin  | Unauthorized update    | Non-admin access           | Blocked            | High     |
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
