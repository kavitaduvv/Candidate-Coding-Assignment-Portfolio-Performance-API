# 📘 Portfolio Management API

A simple REST API for managing investment portfolios, assets, transactions, and performance analytics. Built with ASP.NET Core and SQLite.

---

## 🔗 Base URL

```
http://localhost:5000/api/
```

---
🔹 Authentication
❌ No authentication is required (currently open for local testing)



## 📂 Endpoints Overview

| Resource     | Methods     | URL Format                                |
|--------------|-------------|--------------------------------------------|
| Portfolio    | `GET, POST` | `/api/portfolios`                         |
| Asset        | `GET, POST,PUT, DELETE` | `/api/portfolios/{portfolioId}/assets` |
| Transaction  | `GET, POST` | `/api/assets/{assetId}/transactions`      |
| Performance  | `GET`       | `/api/portfolios/{portfolioId}/performance` |

---

## 📁 Portfolio API

### GET `/api/portfolios`
Returns a list of portfolios.
**Response:**
```json
[
  {
    "id": 1,
    "name": "Growth Portfolio"
  }
]
```

### POST `/api/portfolios`
Create a new portfolio.
**Request Body:**
```json
{
  "name": "Retirement Portfolio"
}
```

**Validations:**
- `name`: required, max 100 characters

**Response:**
```json
{
  "id": 2,
  "name": "Retirement Portfolio"
}
```

---

## 📁 Asset API

### GET `/api/portfolios/{portfolioId}/assets`
Returns all assets in a portfolio.
**Response:**
```json
[
  {
    "id": 1,
    "symbol": "AAPL",
    "type": "Stock"
  }
]
```

### POST `/api/portfolios/{portfolioId}/assets`
Add an asset to a portfolio.
**Request Body:**
```json
{
  "symbol": "TSLA",
  "type": "Stock"
}
```

**Validations:**
- `symbol`: required, max 10 characters
- `type`: required, max 50 characters

**Response:** 200 ok
```json
{
  "id": 2,
  "symbol": "TSLA",
  "type": "Stock",
  "portfolioId": 1
}
```

### PUT `/api/portfolios/{portfolioId}/assets/{id}`

Update asset.
Request Body:
{
  "symbol": "TSLA",
  "type": "Equity"
}


### DELETE `/api/portfolios/{portfolioId}/assets/{id}`

Deletes asset.
Response: 204 No Content
---

## 📁 Transaction API

### GET `/api/assets/{assetId}/transactions`
Returns transactions for an asset.
**Response:**
```json
[
  {
    "id": 1,
    "assetId": 1,
    "date": "2024-07-01T00:00:00Z",
    "quantity": 10,
    "price": 150.00
  }
]
```

### POST `/api/assets/{assetId}/transactions`
Add a transaction to an asset.
**Request Body:**
```json
{
  "date": "2024-07-05",
  "quantity": 5,
  "price": 180.25
}
```

**Validations:**
- `date`: required
- `quantity`: between -1,000,000 and +1,000,000
- `price`: must be > 0

---

## 📈 Performance API

GET /api/portfolios/{portfolioId}/performance?startDate=2024-01-01&endDate=2024-07-01
Calculates gain/loss and total value.
**Response:**
```json
{
  "portfolioId": 1,
  "startDate": "2024-01-01",
  "endDate": "2024-07-01",
  "totalMarketValue": 5400.00,
  "realizedGain": 600.00,
  "unrealizedGain": 200.00,
  "assetBreakdown": [
    {
      "symbol": "AAPL",
      "type": "Stock",
      "quantityHeld": 5,
      "marketValue": 1500.00,
      "costBasis": 1300.00,
      "unrealizedGain": 200.00
    }
  ]
}
```

---

## ❗ Validation Errors
On invalid input (e.g. missing name, too long symbol), the API responds with:
**Example Response:**
```json
{
  "errors": {
    "Name": ["The Name field is required."]
  }
}
```
## How to Run Locally
## Inside the root folder:
dotnet restore
dotnet build
dotnet run --project PortfolioAPI_NoDTO

Then open http://localhost:5000/swagger
## To run tests:
dotnet test PortfolioAPI_NoDTO.Tests

---

## 🛠️ Notes
All dates should be in ISO 8601 format: YYYY-MM-DD

IDs are auto-generated

Swagger UI available at:
http://localhost:5000/swagger
