# Demo Lookup

A synthetic demo dataset for a number-to-info lookup: **10,000 placeholder records**.

Everything here is fictional. Phone numbers look like `DEMO-PHONE-001001`, emails end in `example.invalid`, Aadhaar fields are `AADHAAR-DEMO-…` placeholders, and every record carries `"is_real_person": false`. No real personal or Aadhaar data is included.

## Files

The original single `data2.json` is 7.4 MB, which is larger than the GitHub API allows in one request, so it is stored as three valid-JSON parts. Each part has the same header and its own slice of `users`.

| File | Records | IDs |
|---|---|---|
| `data2-part1.json` | 3,334 | `DEMO-001001` … `DEMO-004334` |
| `data2-part2.json` | 3,334 | `DEMO-004335` … `DEMO-007668` |
| `data2-part3.json` | 3,332 | `DEMO-007669` … `DEMO-011000` |

## Rebuilding the original file

Concatenating the three `users` arrays in order reproduces the original 10,000 records exactly:

```python
import json

users = []
for i in (1, 2, 3):
    with open(f"data2-part{i}.json", encoding="utf-8") as f:
        users += json.load(f)["users"]

assert len(users) == 10000
json.dump(users, open("data2.json", "w", encoding="utf-8"), indent=2, ensure_ascii=False)
```

## Fields

Each record: `id`, `name`, `phone`, `email`, `age`, `date_of_birth`, `gender`, `address`, `occupation`, `preferred_language`, `aadhaar`, `aadhaar_status`, `source`, `is_real_person`.

Searchable on `id`, `phone`, `name`, `aadhaar`.
