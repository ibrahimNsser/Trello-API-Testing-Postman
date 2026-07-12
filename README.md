# 🌐 Trello API Testing using Postman

A comprehensive API testing project for **Trello REST API**. This repository contains Postman collections and environment configurations designed to validate the behavior of Trello's core endpoints (Boards, Lists, and Cards) under various conditions, covering both **Positive** and **Negative** test scenarios.

---

## 🚀 Project Overview

The main objective of this project is to ensure the reliability, security, and stability of Trello's API endpoints. It includes thorough validation of status codes, response bodies, boundary values, and authentication constraints.

### 🛠️ Technologies & Tools Used
* **Postman**: For constructing, organizing, and executing API requests.
* **JavaScript (Postman Scripts)**: Used for writing dynamic assertions and post-response validations.
* **Environments**: Configured dynamic variables (e.g., `{{login_Board_Id}}`, tokens, keys) to avoid hardcoding.

---

## 📁 Collections & Test Coverage

The project is structured into **3 main collections**, each covering exhaustive positive and negative scenarios:

### 1. 📋 Trello API - Create Board Scenarios
Validates the creation of Trello Boards with strict boundary and security checks:
* **Positive**: Create a valid board with required fields.
* **Security & Auth**: Testing requests missing API Keys, Tokens, or required fields.
* **Boundary Value Testing**: 
  * Minimum name length (1 Character).
  * Maximum name length boundary (16,384 Characters).
  * Out-of-bounds validation (16,385 Characters).
* **Error Handling**: Invalid HTTP methods and incorrect endpoints.

### 2. 🗂️ Trello API - Create List Scenarios
Validates the creation of lists inside boards:
* **Positive**: Successfully creating a list with valid data.
* **Validation Checks**: Creating lists without a name, without `Board_id`, or providing an invalid `Board_id`.

### 3. 💳 Trello API - Create Card Scenarios
Tests the integrity of adding cards to specific lists:
* **Positive**: Creating a valid card inside a list.
* **Validation Checks**: Inputting invalid data types in query parameters, requests missing the critical `List_id`, missing authentication keys, or missing security tokens.
* **Error Handling**: Testing invalid HTTP methods (e.g., trying a PUT instead of POST).

---

## 📊 Sample Assertions Implemented

Dynamic scripts are added to the **Post-response** section to automatically validate the API behavior. Examples include:
* Validating standard HTTP status codes (`200 OK`, `400 Bad Request`, `401 Unauthorized`).
* Verifying specific error response messages (e.g., checking if the response body contains `"invalid key"` upon auth failure).

```javascript
pm.test("Status code is 401", function () {
    pm.response.to.have.status(401);
});

pm.test("Check if response contains invalid key", function () {
    pm.expect(pm.response.text()).to.include("invalid key");
});
