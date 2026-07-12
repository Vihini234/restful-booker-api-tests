# Restful Booker API Test Suite 🧪

Automated API testing project built with **Postman**, covering full CRUD operations, authentication, and negative test scenarios against the [Restful Booker API](https://restful-booker.herokuapp.com) — a hotel booking practice API.

## 📋 Project Overview

This project demonstrates end-to-end REST API testing skills, including:

- ✅ Full **CRUD coverage** (Create, Read, Update, Delete)
- 🔐 **Authentication handling** (token-based and Basic auth)
- 🔗 **Request chaining** using environment variables (`bookingId`, `token`)
- 🧪 **Automated assertions** on status codes, response bodies, and data types
- ❌ **Negative testing** (invalid payloads, missing auth, non-existent resources)
- 🖥️ **CLI execution** with Newman

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Postman | Test design & execution |
| JavaScript (pm API) | Test assertions & scripting |
| Newman | Command-line collection runner |
| Restful Booker | System under test |

## 📁 Test Coverage

### Positive Tests

| # | Request | Method | Endpoint | Validations |
|---|---------|--------|----------|-------------|
| 1 | Health Check | GET | `/ping` | Status 201 |
| 2 | Get Auth Token | POST | `/auth` | Status 200, token is a string, token saved to environment |
| 3 | Create Booking | POST | `/booking` | Status 200, `bookingid` returned, booking data matches payload |
| 4 | Get Booking | GET | `/booking/{id}` | Status 200, firstname/lastname correct |
| 5 | Update Booking | PUT | `/booking/{id}` | Status 200, updated fields reflected |
| 6 | Delete Booking | DELETE | `/booking/{id}` | Status 201 (API-specific behavior) |
| 7 | Verify Deletion | GET | `/booking/{id}` | Status 404 after delete |

### Negative Tests

| # | Scenario | Expected Result |
|---|----------|-----------------|
| 1 | Create booking with missing required fields | 500 Internal Server Error |
| 2 | Update booking without auth | 403 Forbidden |
| 3 | Get booking with invalid ID | 404 Not Found |
| 4 | Auth with invalid credentials | Error response (`"reason": "Bad credentials"`) |

## 🔗 Request Chaining

The collection uses environment variables to chain requests, so the suite runs end-to-end without manual input:

```
Get Auth Token  ──▶  saves {{token}}
Create Booking  ──▶  saves {{bookingId}}
Get / Update / Delete  ──▶  reuse {{bookingId}} and {{token}}
```

Example — capturing the booking ID after creation:

```javascript
pm.test("Response has bookingid", () => {
    const json = pm.response.json();
    pm.expect(json.bookingid).to.be.a("number");
    pm.environment.set("bookingId", json.bookingid);
});
```

## 🚀 How to Run

### Option 1 — Postman

1. Import `Restful-Booker-API-Tests.postman_collection.json`
2. Import `New-Environment.postman_environment.json`
3. Select the environment (top-right dropdown)
4. Right-click the collection → **Run collection**

### Option 2 — Newman (CLI)

```bash
# Install Newman
npm install -g newman

# Run the collection
newman run Restful-Booker-API-Tests.postman_collection.json \
  -e New-Environment.postman_environment.json
```

### Option 3 — Newman with HTML report

```bash
npm install -g newman-reporter-htmlextra

newman run Restful-Booker-API-Tests.postman_collection.json \
  -e New-Environment.postman_environment.json \
  -r htmlextra
```

## 📸 Results

<!-- Add your screenshots here -->
![Collection run results](screenshots/collection-run.png)
![Newman CLI output](screenshots/newman-output.png)

## 📌 Key Learnings

- Restful Booker returns **500 instead of 400** for malformed payloads — documenting actual vs. expected API behavior is part of a tester's job
- DELETE returns **201 Created** rather than the conventional 200/204 — a good example of why reading API behavior matters more than assuming standards
- Token-based auth via the `Cookie` header vs. **Basic auth** via the `Authorization` header — both supported, Basic auth is stateless and doesn't expire
- Environment variables make collections **re-runnable and CI-friendly** with zero manual steps

## 🔮 Possible Extensions

- [ ] GitHub Actions workflow to run the suite on every push
- [ ] Data-driven testing with a CSV of booking payloads
- [ ] Schema validation using `pm.response.to.have.jsonSchema()`
- [ ] Performance checks (response time assertions)

---

**Author:** [Your Name] · [LinkedIn](#) · [GitHub](#)
