# 📘 Portfolio Management API

A simple REST API for managing investment portfolios, assets, transactions, and performance analytics.

---

## 🔗 Base URL
http://localhost:5000/api/

---

## 📂 Endpoints Overview

| Resource     | Methods               | URL Format                                |
|--------------|------------------------|--------------------------------------------|
| **Portfolio**    | `GET`, `POST`        | `/api/portfolios`                         |
| **Asset**        | `GET`, `POST`, `PUT`, `DELETE` | `/api/portfolios/{portfolioId}/assets` |
| **Transaction**  | `GET`, `POST`        | `/api/assets/{assetId}/transactions`      |
| **Performance**  | `GET`                | `/api/portfolios/{portfolioId}/performance` |

---

## 📁 Portfolio API

### ➤ `GET /api/portfolios`
Returns all portfolios.
[
  {
    "id": 1,
    "name": "Growth Portfolio"
  }
]

### ➤ `POST /api/portfolios`
Create a new portfolio.
### Request Body
{
  "name": "Retirement Portfolio"
}
### Response
{
  "id": 2,
  "name": "Retirement Portfolio"
}

## 📁 Asset API

### ➤ GET /api/portfolios/{portfolioId}/assets
Returns all assets in a portfolio.
[
  {
    "id": 1,
    "symbol": "AAPL",
    "type": "Stock"
  }
]

### ➤ POST /api/portfolios/{portfolioId}/assets
Add an asset to a portfolio.
### Request Body:
{
  "symbol": "TSLA",
  "type": "Stock"
}
### Response 200 ok 
{
  "id": 2,
  "symbol": "TSLA",
  "type": "Stock",
  "portfolioId": 1
}
### ➤ PUT /api/portfolios/{portfolioId}/assets/{id}
Update an asset.
###  Request Body:
{
  "symbol": "TSLA",
  "type": "Equity"
}
### ➤ DELETE /api/portfolios/{portfolioId}/assets/{id}
Deletes the specified asset.
### Response: 204 No Content

## 📁  Transaction API
### ➤ GET /api/assets/{assetId}/transactions
Returns transactions for an asset.
### Response
[
  {
    "id": 1,
    "assetId": 1,
    "date": "2024-07-01T00:00:00Z",
    "quantity": 10,
    "price": 150.00
  }
]
### ➤ POST /api/assets/{assetId}/transactions
Add a transaction to an asset.
###  Request Body
{
  "date": "2024-07-05",
  "quantity": 5,
  "price": 180.25
}
### Validations:
date: required
quantity: between -1,000,000 and +1,000,000
price: must be > 0

## 📁  Performance API
### ➤ GET /api/portfolios/{portfolioId}/performance?startDate=2024-01-01&endDate=2024-07-01
Calculates gain/loss and total value.
### Response:
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
### ❗ Validation Errors
On invalid input (e.g. missing name, too long symbol), the API responds with:
{
  "errors": {
    "Name": [
      "The Name field is required."
    ]
  }
}

## 🛠️ Developer Notes
### 🌐 Swagger UI: http://localhost:5000/swagger
### 💾 Database: SQLite portfolio.db
### 📦 Testable via dotnet test
### 🧪 Unit test coverage for all controllers & validation
### 📦 Tech Stack
### ASP.NET Core 8.0
### Entity Framework Core (SQLite/InMemory)
### xUnit for testing
### Swagger for docs
## 📁 Project Structure

### PortfolioAPI_NoDTO/

### ├── Controllers/
### ├── Models/
### ├── PortfolioAPI_NoDTO.csproj
### ├── Program.cs
### ├── AppDbContext.cs
### ├── SampleDataSeeder.cs
### ├── README.md



