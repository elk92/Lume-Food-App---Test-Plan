# Test Plan – LumeFood

## 1. Overview

This document defines the testing strategy, scope, risks, and high level test scenarios for the LumeFood app.

---

## 2. Test Scope

### In Scope
- Authentication
- User register
- Restaurant listing
- Product catalog
- Orders
- Cart management
- Checkout process

### Out of Scope
- Real payment integrations
- Advanced security testing

---

## 3. Test Types

| Test Type        | Description |
|------------------|------------|
| Functional       | Validate business flows |
| API Testing      | Validate backend endpoints |
| Integration      | Validate system interactions |
| Performance      | Validate response time and load |
| Usability        | Validate user experience and responsive layout |

---

## 4. Risks & Attention Points

| Area        | Risk Level | Description |
|------------|-----------|------------|
| Checkout   | High      | Financial impact if broken |
| Login      | High      | User access issues |
| Cart       | High      | Core functionality |
| Order      | High      | Order list and details fuctionalities |
| Catalog    | Medium    | Catalog list |
| API        | High      | Data inconsistency |
| UI         | Low       | Visual issues |

---

## 5. Test Scenarios (High-Level)

| ID  | Feature       | Scenario                          | Type        | Priority |
|-----|--------------|-----------------------------------|------------|----------|
| TC01| Login        | Login with valid credentials      | Functional | High     |
| TC02| Login        | Login with invalid credentials    | Functional | High     |
| TC01| Login        | Login with expired credentials    | Edge Case  | High     |
| TC03| Catalog      | List restaurants                  | Functional | Medium   |
| TC04| Order        | List orders                       | Functional | Medium   |
| TC05| Product      | View restaurants details          | Functional | Medium   |
| TC06| Cart         | Add item to cart                  | Functional | High     |
| TC07| Cart         | Remove item from cart             | Functional | High     |
| TC08| Checkout     | Complete order successfully       | Functional | High     |
| TC09| Checkout     | Checkout with empty cart          | Edge Case  | High     |
| TC10| Register     | Complete user register successfully | Functional | High     |
| TC11| API          | Login API returns token           | API        | High     |
| TC12| Performance  | Non-functional Tests before v1    | Performance| Medium   |
---

## 6. Entry Criteria

- Application is deployed
- Environment is stable

---

## 7. Exit Criteria

- Critical tests passed
- No blocking bugs
- Non-functionals tests scenarios accetable results
