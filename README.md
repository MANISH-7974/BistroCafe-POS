# BistroCafe POS

BistroCafe POS is a college-level web-based restaurant Point-of-Sale and management system. It combines menu ordering, cart-based billing, inventory validation, PDF receipt generation, optional email delivery and an administrator dashboard in one lightweight Flask application.

The project is designed for academic demonstration and small single-process deployments. It intentionally focuses on the core restaurant-counter workflow rather than enterprise features.

## Live application

**Hosted application:** [Open BistroCafe POS](https://bistrocafe-jsfgtwop.manus.space)

**Project demonstration video:** Add the public video URL here after uploading `BistroCafe_Project_Demonstration.mp4` to an approved platform.

## Main features

- Categorized menu browsing with search support
- Cart-based order creation and quantity controls
- Cash, UPI and Card payment-method selection
- Customer name, email and table/order reference fields
- Discount, GST, subtotal and grand-total calculation
- Server-side menu-price and stock validation
- Low-stock and out-of-stock inventory alerts
- Branded A5 customer receipt PDF generation
- Optional SMTP email receipt with PDF attachment
- Protected administrator login
- Sales KPIs, recent orders and product-mix analytics
- Inventory update controls and CSV sales export
- Responsive current-order panel with open/close control
- Docker and Gunicorn deployment configuration

## Technology stack

- **Backend:** Python 3.12, Flask 3.1
- **Frontend:** HTML5, CSS3 and JavaScript
- **Storage:** JSON inventory file, CSV sales records and local PDF files
- **PDF generation:** FPDF
- **Email delivery:** Python SMTP libraries
- **Authentication:** Flask session with Werkzeug password hashing
- **Deployment:** Docker and Gunicorn

## Repository structure

```text
.
├── app.py                         # Flask routes and business logic
├── index.html                     # POS terminal frontend
├── admin.html                     # Administrator dashboard
├── login.html                     # Administrator login page
├── inventory.json                 # Safe demonstration inventory data
├── daily_sales.example.csv        # Sample CSV schema without runtime records
├── requirements.txt               # Pinned Python dependencies
├── Dockerfile                     # Production container configuration
├── .dockerignore                  # Container build exclusions
├── .gitignore                     # Git exclusions for secrets and runtime data
├── .env.example                   # Placeholder environment configuration
├── static/
│   └── bistrocafe-logo.png        # Shared project logo
└── docs/
    ├── SDMS_Submission_Content.md
    ├── BistroCafe_SDMS_Submission_Content.docx
    └── screenshots/               # Five SDMS-ready screenshots
```

## Run locally on Windows

Open PowerShell in the repository folder:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
Copy-Item .env.example .env
python app.py
```

Open the application at:

```text
http://127.0.0.1:5000
```

If PowerShell blocks virtual-environment activation for the current session:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

## Environment configuration

Create a local `.env` file beside `app.py`. The `.env` file is intentionally ignored by Git and must never be uploaded publicly.

```env
APP_ENV=development
FLASK_DEBUG=0
FLASK_SECRET_KEY=create-a-long-random-local-secret
ADMIN_USERNAME=choose-a-local-admin-username
ADMIN_PASSWORD=choose-a-local-demo-password
ADMIN_PASSWORD_HASH=
SMTP_SENDER_EMAIL=your-email@example.com
SMTP_APP_PASSWORD=provider-app-password-only-if-email-is-required
```

For production, use a protected secret manager and prefer `ADMIN_PASSWORD_HASH` instead of storing a plain administrator password. Email delivery is optional; the PDF receipt can still be downloaded when SMTP is not configured.

## Docker deployment

Build the image:

```bash
docker build -t bistrocafe-pos .
```

Run it with a local environment file:

```bash
docker run --rm -p 3000:3000 --env-file .env bistrocafe-pos
```

Open:

```text
http://127.0.0.1:3000
```

The container uses Gunicorn and listens on the `PORT` environment variable, defaulting to port `3000`.

## Data and academic scope

The demonstration version uses JSON, CSV and local invoice-file storage so that the architecture remains easy to understand and run for a college project. A production business deployment should migrate orders and inventory to a transactional database and use persistent object storage for receipts.

The project does not include online payment settlement, delivery tracking, order-status workflows, multi-branch synchronization, customer accounts or enterprise accounting integration.

## Security and public-repository rules

Never commit any of the following:

- `.env` files
- Flask secret keys
- Administrator passwords or password hashes
- SMTP usernames or app passwords
- Real customer records
- Private invoices or runtime sales exports

Before making the repository public, revoke any previously exposed SMTP app password and create a new one if email testing is still required.

## Documentation and screenshots

The `docs/` directory contains the SDMS submission content and five compressed screenshots with captions. The screenshots are intended for academic documentation and should be inserted into the relevant report sections with their captions.

## Limitations and future scope

The current project is intentionally limited to a small single-process restaurant workflow. Future versions may add a managed database, persistent object storage, role-based access, audit logging, online payment integration, automated backups and a kitchen display.

## Academic project note

This repository is provided for educational demonstration and final project evaluation. Replace placeholder student, guide, department and institution details before submission.
