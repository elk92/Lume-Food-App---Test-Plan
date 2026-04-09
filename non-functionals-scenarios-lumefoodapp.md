# Non-Functional Test Scenarios – LumeFood

## 1. Overview

This document defines non-functional test scenarios focused on performance, load, and stress testing for the LumeFood app before production release.

---

## 2. Objectives

- Ensure system stability under expected and peak load conditions
- Identify performance bottlenecks
- Validate system behavior under stress
- Guarantee acceptable response times for critical flows

---

## 3. Performance Criteria

| Metric                  | Target Value        |
|------------------------|---------------------|
| API Response Time      | < 500ms             |
| Page Load Time         | < 2s                |
| Error Rate             | < 1%                |
| Throughput             | Stable under load   |

---

## 4. Load Testing Scenarios

### 📌 LT01 – Restaurant Listing Load

| ID   | Scenario Description |
|------|---------------------|
| LT01 | Simulate 500 concurrent users accessing restaurant list |

**Steps:**
- Send concurrent GET requests to `/restaurantes`
- Maintain load for 5 minutes

**Expected Results:**
- Response time < 500ms
- No errors or timeouts
- Stable throughput

---

### 📌 LT02 – Product Listing Load

| ID   | Scenario Description |
|------|---------------------|
| LT02 | Simulate 300 users browsing products |

**Steps:**
- Access `/products` endpoint repeatedly
- Simulate user navigation behavior

**Expected Results:**
- No degradation in performance
- Consistent response times

---

### 📌 LT03 – Add to Cart Load

| ID   | Scenario Description |
|------|---------------------|
| LT03 | Simulate 200 users adding items to cart simultaneously |

**Steps:**
- Execute POST `/cart` requests
- Repeat actions per user session

**Expected Results:**
- Cart updates correctly
- No data inconsistency
- Response time within acceptable limits

---

### 📌 LT04 – Checkout Load (Critical)

| ID   | Scenario Description |
|------|---------------------|
| LT04 | Simulate 100 concurrent checkout operations |

**Steps:**
- Execute full checkout flow via API
- Include authentication and order creation

**Expected Results:**
- Orders created successfully
- No duplicate or failed orders
- Response time < 800ms

---

## 5. Stress Testing Scenarios

### 📌 ST01 – System Overload

| ID   | Scenario Description |
|------|---------------------|
| ST01 | Gradually increases the app users until system failure |

**Steps:**
- Start with 100 users
- Increase by 100 every minute
- Continue until system degrades

**Expected Results:**
- System fails gracefully
- No data corruption
- Proper error responses returned

---

### 📌 ST02 – Spike Traffic

| ID   | Scenario Description |
|------|---------------------|
| ST02 | Simulate sudden spike of 1000 users |

**Steps:**
- Instantly generate 1000 concurrent requests
- Target `/restaurants` and `/checkout`

**Expected Results:**
- System handles spike or degrades gracefully
- No crashes
- Acceptable error handling

---

### 📌 ST03 – Checkout Failure Under Load

| ID   | Scenario Description |
|------|---------------------|
| ST03 | Simulate checkout under extreme load |

**Steps:**
- Execute 300 concurrent checkout requests
- Introduce artificial latency

**Expected Results:**
- No duplicate orders
- Transactions remain consistent
- Failures handled correctly

---

### 📌 ST04 – Long Duration Stability (Soak Test)

| ID   | Scenario Description |
|------|---------------------|
| ST04 | Run system under moderate load for extended period |

**Steps:**
- Maintain 200 users for 2 hours
- Monitor memory and CPU usage

**Expected Results:**
- No memory leaks
- Stable performance over time
- No degradation

---

## 6. Monitoring & Metrics

During execution, monitor:

- CPU usage
- Memory usage
- API latency
- Error rates
- Throughput

---

## 7. Risks & Attention Points

| Area        | Risk |
|------------|------|
| Checkout   | High risk of failure under load |
| Database   | Bottlenecks in high concurrency |
| API        | Timeout and latency issues |
| Cart       | Data inconsistency |

---

## 8. Tools Suggested

- k6
- JMeter

---

## 9. Exit Criteria

- All critical flows meet performance thresholds
- No critical failures under load
- System degrades gracefully under stress
