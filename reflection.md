SRN: PES2UG24AM034

# Reflection

**1. Which tool was most useful and why?**
Bandit surfaced the most serious problem (command injection via `os.system`), which neither Pylint nor Flake8 mention. Pylint gave the biggest improvement in maintainability (mutable default, unused argument, naming, docstrings). Flake8 was quick and mechanical, covering formatting only.

**2. Which issues were hardest to fix, and why?**
The shell injection needed a design change rather than a rename: validate the IP and replace `curl` through `os.system` with `http.client`. The mutable default needed the `None` pattern so each call gets its own dict.

**3. Were there false positives or issues you chose not to fix?**
No suppressions were needed. The hard-coded "password" was unused demo data, so it was removed rather than ignored.

**4. How does static analysis help code quality, and how would you use it in future?**
It catches bugs, security holes and style problems without running the code, and enforces consistency. I would run all three tools in a pre-commit hook or CI pipeline so problems are caught before merge.
