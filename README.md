# Restful Booker — API Test Collection

Postman test suite for the [Restful Booker API](https://restful-booker.herokuapp.com/apidoc) —
a hotel booking REST API — covering authentication, full CRUD operations,
and negative scenarios.

> 🔨 **Status: In progress** — collection under active development.
<!-- When finished, replace the line above with: ✅ Status: Complete -->

---

## What this project demonstrates

- API testing fundamentals: HTTP methods, status codes, headers, JSON payloads
- Positive **and** negative test design (missing fields, invalid IDs, missing/invalid auth tokens)
- Request chaining with environment variables (auth `token` and `bookingId`
  captured from responses and reused in later requests)
- Automated assertions on status codes, response body values, and response time

## Collection structure

| Folder | Covers |
|--------|--------|
| Health | API availability check (ping) |
| Auth | Token creation — valid and invalid credentials |
| Bookings – GET | All bookings, by ID, filtered search, invalid ID handling |
| Bookings – POST | Valid creation, missing required fields, wrong data types |
| Bookings – PUT/PATCH | Full and partial updates, with/without auth token |
| Bookings – DELETE | Valid deletion, repeat deletion, missing token |

## How to run

1. Import both JSON files into Postman:
   - `collection/Restful-Booker-API-Tests.postman_collection.json`
   - `environment/Restful-Booker.postman_environment.json`
2. Select the **Restful Booker** environment
3. Run the collection with Collection Runner (Auth folder runs first —
   later requests depend on the token it captures)

## Findings — observed vs expected behavior

<!-- Fill this as you test. Examples of the kind of thing you'll find: -->
<!-- - POST with missing required field returns 500; a 400 Bad Request would be expected -->
<!-- - Invalid token on PUT returns 403 Forbidden (expected behavior confirmed) -->
_To be documented during testing._

## Results

<!-- After your final Collection Runner pass: -->
<!-- ![Collection Runner results](screenshots/collection-runner-results.png) -->
_Run results will be added on completion._

📖 **Published collection documentation:** _link coming on completion_
<!-- Replace with your public Postman docs link -->

---

*Part of my QA portfolio — see also:
[SauceDemo Manual Testing](https://github.com/Vihini234/QA-Portfolio)*
