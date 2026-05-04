# ITPM — Assignment 1 — IT23183704

This repository contains `test_automation`, a Python-based frontend test automation tool that automates evaluation of the Pixelssuite Chat Translator (Singlish → Sinhala). The script reads test rows from an Excel workbook, sends Singlish inputs to the web frontend, captures the actual Sinhala output, and writes results back into the workbook.

✨ Features

- **Browser Automation:** Playwright-driven Chromium automation for reliable UI interaction.
- **Smart Excel Parsing:** Auto-detects header row and maps common column names (`Input`, `Expected`, etc.).
- **Retry & Robustness:** Configurable retries and waits for slow networks or delayed UI updates.
- **Progressive Saving:** Optionally save results after every N tests to avoid data loss.
- **Overlay Dismissal:** Attempts to auto-click cookie/consent popups and dismiss overlays.
- **Headless / Manual Modes:** Run with or without browser GUI; use slow-mo / keep-open for manual inspection.

🗂️ Project Structure

```
test_automation/
├── test_automation.py        # Main Playwright automation script
├── Assignment 1 - Test cases.xlsx  # Example Excel test workbook (optional)
└── README.md                 # This file
```

⚙️ Prerequisites

- Python 3.8 or newer
- Google Chrome (recommended) or Chromium
- `pip` package manager

🚀 Installation

Step 1 — Clone the repository

```bash
git clone <your-repo-url>
cd test_automation
```

Step 2 — Install Python dependencies

```bash
pip install playwright openpyxl
```

Step 3 — Install Playwright browser binaries

```bash
python -m playwright install
```

▶️ Running the Tests

✅ Recommended Command (interactive / watchable run)

```bash
python test_automation/test_automation.py \
	--excel "Assignment 1 - Test cases.xlsx" \
	--input-col "Input" \
	--url "https://www.pixelssuite.com/chat-translator" \
	--wait-ms 7000 \
	--retry-wait-ms 1500 \
	--retries 8 \
	--type-delay-ms 50 \
	--slow-mo-ms 200 \
	--save-every 1
```

Important: Close the Excel file in Excel before running the script (Excel locks files).

🐢 Slow Connection (increase waits/retries)

```bash
python test_automation/test_automation.py --excel "Assignment 1 - Test cases.xlsx" --wait-ms 10000 --retry-wait-ms 2000 --retries 10
```

🔍 Manual Inspection Mode (keep browser open)

```bash
python test_automation/test_automation.py --excel "Assignment 1 - Test cases.xlsx" --slow-mo-ms 500 --keep-open
```

🧾 Command-Line Options (quick reference)

- `--excel` (default: `Assignment 1 - Test cases.xlsx`) — Path to Excel test case file
- `--sheet` (default: ` Test cases`) — Worksheet name (note: leading space in default)
- `--input-col` — Column name for Singlish input (auto-detected if omitted)
- `--expected-col` — Column name for expected Sinhala output (auto-detected)
- `--actual-col` — Column name for actual output (created if missing)
- `--status-col` — Column name for test status (created if missing)
- `--url` (default: `https://www.pixelssuite.com/chat-translator`) — Target application URL
- `--wait-ms` (default: `5000`) — Wait time after submission (ms)
- `--retry-wait-ms` (default: `1000`) — Wait between retries (ms)
- `--retries` (default: `8`) — Number of retry attempts for capturing output
- `--type-delay-ms` (default: `30`) — Per-keystroke delay (ms)
- `--slow-mo-ms` (default: `0`) — Global slow-motion delay (ms)
- `--timeout-ms` (default: `60000`) — Overall UI timeout (ms)
- `--save-every` (default: `0`) — Save after every N tests (0 = save at end)
- `--headless` — Run browser without GUI
- `--keep-open` — Keep browser open after tests

📋 Excel File Format

The script tries to auto-detect the header row and common column names. At minimum, include a column that contains your Singlish test inputs (e.g. `Input`, `Singlish`, `Test Input`) and — if you have expected outputs — a column for expected Sinhala (e.g. `Expected`, `Sinhala`). The script will create `Actual output` and `Status` columns if they are missing.

Suggested columns (not all required): `TC ID`, `Input length type`, `Input`, `Expected output`, `Actual output`, `Status`, `Singlish input types covered`, `Evidence or rationale`

Status values written by the script:

- `PASS` — Actual output exactly matches expected
- `FAIL` — Actual output does not match expected
- `COLLECTED` — Actual output captured, no expected value provided
- `UI Error` — Interaction failed or element not found

🧪 Test Coverage

This project is typically used with a test workbook covering a set of negative cases for the Pixelssuite Chat Translator. Example usage targets 50 negative test cases spanning 24 Singlish input types (questions, commands, greetings, spelling variants, numbers, emojis, place/person names, etc.). Adjust your workbook to match the categories you want to validate.

🔧 Troubleshooting

- Excel file locked: Close the workbook before running the script.
- Output not captured: Increase `--wait-ms` and/or `--retries`.
- Chrome/Chromium missing: Run `python -m playwright install chromium`.
- Elements not found: Verify the `--url`, increase `--timeout-ms`, or inspect the page to confirm selectors.

👤 Student Information

- **Registration Number:** IT23183704
- **Name:** Liyanage S. T
- **Course / Assignment:** ITPM — Assignment 1

---

