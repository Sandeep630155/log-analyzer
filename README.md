# Log Analysis & Suspicious Activity Detector

Analyzes system/server authentication logs to identify suspicious activity —
repeated failed logins, unusual IP activity, credential stuffing, off-hours
access, and account lockouts — and surfaces them in a Flask dashboard backed
by SQLite.

**Stack:** Python, SQL (SQLite), Pandas, Flask

## What it does

- **Generates realistic demo logs** (`log_generator.py`) simulating normal
  business traffic plus several deliberately injected attack patterns.
- **Parses & analyzes logs with pandas** (`analyzer.py`) using rolling
  time-window logic to flag:
  - `BRUTE_FORCE` – many failed logins against one user from one IP
  - `CREDENTIAL_STUFFING` – one IP trying many different usernames
  - `UNUSUAL_IP_SUCCESS` – a successful login from a never-before-seen IP
  - `OFF_HOURS_ACCESS` – successful logins between midnight and 5am
  - `ACCOUNT_LOCKOUT` – accounts locked after repeated failures
- **Persists everything to SQLite** (`database.py`) — raw logs and alerts.
- **Displays results in a Flask dashboard** (`app.py` + `templates/`) with
  summary stats, an alerts table, and a raw log browser.

## Setup

\`\`\`bash
python -m venv venv
source venv/bin/activate        # Windows: venv\\Scripts\\activate
pip install -r requirements.txt
\`\`\`

## Run

\`\`\`bash
python app.py
\`\`\`

Then open **http://localhost:5000**. On first run it automatically generates
demo log data and runs the detectors. Use the **"Regenerate demo data"**
button in the nav bar any time to generate a fresh batch of logs and re-run
detection.

## Notes

This is a **demo/portfolio project**: all log data is synthetically
generated for illustration and does not reflect any real system or user.
