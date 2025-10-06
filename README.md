 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
index 5b86633d420531969bb684085b6530e4bb55f607..97f332f0f13028cacd249f532d85d706e28c5fb3 100644
--- a/README.md
+++ b/README.md
@@ -1,50 +1,59 @@
 # Finance Modelling Flask App
 
 A modular Flask web app to fetch financial data from Yahoo Finance, build Income Statement / Balance Sheet / Cash Flow,
 run Financial Statement Analysis (ratios, growth, DuPont, common-size), and perform Valuation (DCF + Comparable Multiples).
 It also includes a **one-pager dashboard** and an optional **Live Football Analysis** module.
 
 ## Quick Start
 
 1. **Clone / unzip** this folder.
 2. **Python 3.10+** recommended. Create a virtual env and install dependencies:
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # Windows: .venv\\Scripts\\activate
    pip install -r requirements.txt
    ```
 3. Copy `.env.example` to `.env` and set values (optional; only needed for the sports API or advanced config).
 4. Run the app:
    ```bash
    export FLASK_APP=app.py
    flask run --debug
    # or
    python app.py
    ```
 5. Open **http://127.0.0.1:5000**
 
+### Run the CSR dashboard locally
+
+1. Start the Flask server using the steps above.
+2. Navigate to **http://127.0.0.1:5000/csr** in your browser.
+3. Use the sample workbook at `data/sample_csr_dashboard.xlsx` (included in the repo) to try the dashboard immediately.
+4. After uploading you can switch between the seeded companies, toggle descriptive statistics / the correlation matrix, and confirm the charts render correctly.
+
+> Tip: Replace the sample workbook with your own .xlsx file that follows the same column layout to analyse different companies.
+
 ## What makes this different
 - **Step-by-step pipeline UI:** Ingestion → Statements → Analysis → Valuation → One-Pager → Export.
 - **Download everything:** Raw data, standardized statements, ratio tables, and model outputs (CSV/XLSX).
 - **Common-size + DuPont + Quality-of-Earnings** checks out-of-the-box.
 - **Scenario Manager** for DCF (base/optimistic/pessimistic) and **Monte Carlo** (optional extension placeholder).
 - **Upload fallback:** If Yahoo Finance fails, upload your own XLSX and continue the same pipeline.
 - **API-first:** Clean JSON endpoints for using the engine from other apps.
 - **Sports add-on:** Example blueprint showing how to add a live football page via an external API (plug your key).
 
 ## Structure
 ```
 finance-flask-app/
 ├─ app.py
 ├─ requirements.txt
 ├─ .env.example
 ├─ routes/
 │  ├─ __init__.py
 │  ├─ data_routes.py
 │  ├─ statements_routes.py
 │  ├─ analysis_routes.py
 │  ├─ valuation_routes.py
 │  └─ sports_routes.py
 ├─ services/
 │  ├─ __init__.py
 │  ├─ data_fetch.py
 
EOF
)