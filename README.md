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

### ➤ `POST /api/portfolios`

**Body:**
```json
{
  "name": "My Portfolio"
}
Validations:

name: Required, max 100 characters

📁 Asset API
➤ GET /api/portfolios/{portfolioId}/assets
Returns assets in a portfolio.

➤ POST /api/portfolios/{portfolioId}/assets
json
{
  "symbol": "AAPL",
  "type": "Stock"
}
Validations:

symbol: Required, max 10 characters

type: Required, max 50 characters

📈 Performance API
➤ GET /api/portfolios/{portfolioId}/performance
With query params:
?startDate=2024-01-01&endDate=2024-07-01
Returns portfolio valuation, realized/unrealized gains, and asset breakdown.

❗ Validation Errors
{
  "errors": {
    "Symbol": ["Symbol is required and cannot exceed 10 characters."]
  }
}

🛠️ Developer Notes
🌐 Swagger UI: http://localhost:5000/swagger

💾 Database: SQLite portfolio.db

📦 Testable via dotnet test

🧪 Unit test coverage for all controllers & validation

📦 Tech Stack
ASP.NET Core 8.0

Entity Framework Core (SQLite/InMemory)

xUnit for testing

Swagger for docs

📁 Project Structure
PortfolioAPI_NoDTO/
│
├── Controllers/
├── Models/
├── PortfolioAPI_NoDTO.csproj
├── Program.cs
├── AppDbContext.cs
├── SampleDataSeeder.cs
├── README.md

