# grocx

Give it a grocery list and it chooses which quick-commerce app to buy each item from so the basket is cheapest, including discounts.

You send the items. The optimizer compares prices across the apps, applies each discount, and returns one basket: every item assigned to the app that makes the total lowest, plus how much you save.

## Optimizer, cache, and API

- **Optimizer.** For each item it picks the app with the lowest price after discount, then totals the basket and the savings.
- **Cache.** Prices and discounts sit in a short-lived cache, so a repeat lookup does not fetch the same product again.
- **API.** `POST /api/v1/get_prices` takes the grocery list and returns the optimized basket.

## How to run

### Prerequisites

- Python 3.9+
- pip

### Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/LifeAyush/grocx.git
   cd grocx
   ```

2. Create and activate a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file from the example:

   ```bash
   cp .env.example .env
   ```

### Running locally

```bash
uvicorn app.main:app --reload
```

The API is at http://localhost:8000. Interactive docs are at http://localhost:8000/docs.

### Request

`POST /api/v1/get_prices`

```json
{
  "items": [
    {"name": "Milk", "quantity": 1, "unit": "liter"},
    {"name": "Bread", "quantity": 2, "unit": "loaf"},
    {"name": "Eggs", "quantity": 12, "unit": "piece"}
  ]
}
```

The response includes `total_price`, `savings`, and each item with the chosen app, original price, discount, and final price.

## Testing

```bash
pytest
```

Run tests with coverage:

```bash
pytest --cov=app
```
