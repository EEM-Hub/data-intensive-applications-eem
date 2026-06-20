---
schema_version: "1.0"
type: eem
project_name: "data-intensive-applications-eem"
domain: ["Data Intensive Applications"]
license: cc-by-sa-4.0
base_network: null
source_repos: []
beliefs_total: 1134
beliefs_in: 1009
beliefs_out: 125
premises: 762
derived: 372
nogoods: 0
generator: ftl-reasons/0.48.0
---

# Data Intensive Applications EEM

## Stats

| Metric | Value |
|--------|-------|
| Total beliefs | 1134 |
| Status | 1009 IN / 125 OUT |
| Premises (observations) | 762 |
| Derived (justified conclusions) | 372 |
| Nogoods (contradictions) | 0 |
| Retraction rate | 11% |
| Max derivation depth | 18 |

## How to Use

### Import into a reasons database

```bash
reasons init
reasons import-json network.json
```

### Query beliefs

```bash
reasons search "your query"
reasons explain <node-id>
reasons show <node-id>
```

## Files

| File | Description |
|------|-------------|
| `network.json` | Full belief network (machine-readable, portable) |
| `reasons.db` | SQLite database (gitignored, regenerate with `reasons import-json network.json`) |
| `README.md` | This EEM card |

## Quality

- 1009 beliefs IN, 125 OUT
- 762 premises grounded in direct observations
- 372 derived beliefs justified via SL justifications
- 0 nogoods detected

## Limitations

- Auto-generated card — review and customize for your use case

## License

Sources and entries are derived from Wikipedia articles and licensed under
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
See [LICENSE](LICENSE) and [ATTRIBUTION.md](ATTRIBUTION.md) for details.
