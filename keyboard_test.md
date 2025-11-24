# Keyboard Test File

This file is designed to test your split keyboard layout, specifically for SQL, Python, Markdown, and JSON.

## 1. General Typing & Symbols

The quick brown fox jumps over the lazy dog.
THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG.
1234567890
!@#$%^&*()_+-=[]\{}|;':",./<>?`~

## 2. SQL (Snowflake)

```sql
WITH monthly_sales AS (
    SELECT
        DATE_TRUNC('MONTH', order_date) AS sales_month,
        product_id,
        SUM(quantity * unit_price) AS total_revenue
    FROM sales.orders
    WHERE order_status = 'COMPLETED'
      AND order_date >= '2023-01-01'
    GROUP BY 1, 2
)
SELECT
    ms.sales_month,
    p.product_name,
    ms.total_revenue,
    LAG(ms.total_revenue) OVER (PARTITION BY ms.product_id ORDER BY ms.sales_month) AS prev_month_revenue
FROM monthly_sales ms
JOIN inventory.products p ON ms.product_id = p.id
ORDER BY ms.sales_month DESC, ms.total_revenue DESC;
```

## 3. Python

```python
import json
from datetime import datetime

def process_data(data_list, options=None):
    """
    Process a list of data items.
    """
    if options is None:
        options = {}
    
    results = []
    for item in data_list:
        if item.get('active') and item['value'] > 0:
            processed = {
                'id': item['id'],
                'timestamp': datetime.now().isoformat(),
                'score': item['value'] * 1.5,
                'tags': [t.lower() for t in item.get('tags', [])]
            }
            results.append(processed)
            
    return results

class ConfigLoader:
    def __init__(self, path):
        self.path = path
        self._config = {}

    def load(self):
        with open(self.path, 'r') as f:
            self._config = json.load(f)
```

## 4. JSON

```json
{
  "project": "keyboard_firmware",
  "version": 1.0,
  "features": {
    "split": true,
    "bluetooth": true,
    "layers": [
      "default",
      "lower",
      "raise",
      "adjust"
    ]
  },
  "keymap": [
    {
      "keys": ["Q", "W", "E", "R", "T", "Y", "U", "I", "O", "P"],
      "mod_tap": true
    }
  ],
  "null_check": null
}
```

## 5. Markdown Syntax

- [x] Task 1
- [ ] Task 2
  - Nested item
  
> Blockquote for testing quotes and indentation.

**Bold Text** and *Italic Text* and `Inline Code`.

Link: [ZMK Firmware](https://zmk.dev)
