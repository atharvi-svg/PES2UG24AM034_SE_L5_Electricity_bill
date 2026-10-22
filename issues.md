SRN: PES2UG24AM034

# Lab 5 – Issue Table (electricity_bill.py)

Pylint 5.44/10 → 10.00/10 | Bandit 4 findings → 0 | Flake8 4 findings → 0

| Issue | Type | Line(s) | Description | Fix Approach |
| ----- | ---- | ------- | ----------- | ------------ |
| Shell command injection (B605) | Security – High | 63 | `os.system("curl http://" + meterIp + ...)` builds a shell command from an unvalidated string; input like `1.2.3.4; rm -rf ~` runs arbitrary commands. | Validate with `ipaddress.ip_address()` and fetch with `http.client` – no shell, no external process. |
| Unsafe XML parsing (B314) | Security – Medium | 18 | `ET.fromstring` on untrusted XML is vulnerable to XML attacks (entity expansion). | Use `defusedxml.ElementTree`. |
| Unsafe XML import (B405) | Security – Low | 3 | Importing `xml.etree.ElementTree` is flagged for the same reason. | Import from `defusedxml` instead. |
| Hard-coded password (B105) | Security – Low | 13 | `CLERK_PASSWORD = "bill-desk-demo"` stored in source (and unused). | Removed the constant. |
| Mutable default argument (W0102) | Bug – Medium | 42 | `extras={}` is shared across calls. | Default to `None`, create a new dict inside the function. |
| Unused argument (W0613) | Code smell | 50 | `averageBill(currency)` never uses `currency`. | Removed the parameter and updated the caller. |
| `open()` without encoding (W1514) | Portability | 57 | Encoding depends on platform default. | Added `encoding="utf-8"`. |
| Naming style (C0103) ×14 | Style | 17–67 | camelCase names (`readMeters`, `taxRate`, `slabUnits`, ...). | Renamed to snake_case. |
| Missing docstrings (C0114/C0116) | Style | 1 + all functions | No module/function docstrings. | Added docstrings. |
| Formatting E302, E203, E501, E225 | Style (Flake8) | 22, 44, 72, 76 | Missing blank line, space before `:`, line > 79 chars, missing spaces around `=`. | Reformatted to PEP 8. |
| `main()` runs on import | Design | 82 | Importing the module executes the demo. | Added `if __name__ == "__main__":` guard. |

## Commits
1. Fix Bandit issues (B605, B314, B405, B105)
2. Fix Pylint issues (W0102, W0613, W1514, C0103, C0114, C0116)
3. Fix Flake8 formatting issues (E302, E203, E501, E225) + final reports
