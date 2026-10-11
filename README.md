# Citadel — Enterprise Vulnerability Management & Risk Dashboard

[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688.svg?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-19-61DAFB.svg?logo=react&logoColor=black)](https://react.dev)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-v4-38B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Citadel** is a high-density, enterprise-grade Vulnerability Management and Remediation platform inspired by platforms like **Brinqa**. It unifies vulnerability telemetry from Qualys VMDR, CrowdStrike, and Cloud Posture feeds to automate risk scoring, enforce remediation SLAs, and provide Big 4 audit readiness.

---

## Key Features

- **Prioritization Logic Engine**  
  Computes contextual composite risk scores rather than relying solely on static CVSS:  
  $$\text{Composite Risk} = \text{Base CVSS} + (\text{EPSS} \times 2.0) + \text{Exposure Offset (+1.0)} + \text{Asset Criticality (+0.5 to +1.5)}$$

- **Enterprise SLA Governance**  
  Automates compliance windows across severity tiers (**Critical**: 14d, **High**: 30d, **Medium**: 60d, **Low**: 90d) with real-time status tracking (*Within SLA*, *Out of SLA*, *Met SLA*, *Exceeded SLA*).

- **High-Density Remediation Worklist**  
  High-throughput operations table supporting global search, multi-vector filtering (Business Unit, Owner, Severity, CISA KEV, Public Exposure), and inline status workflows.

- **In-Line Remediation & Audit Trail Drawer**  
  Drill into individual findings to review CVSS/EPSS telemetry, execute status transitions, manage formal exception requests with expiry dates, queue automated retests, and inspect immutable audit event logs.

- **Dual Theme System**  
  Features a custom pill-shaped toggle switch seamlessly switching between **Navy & Gold** (*Default / Advisory Light Mode*) and **Midnight Obsidian** (*SOC Dark Mode*).

- **Big 4 / EY Control Mapping & PDF Exporter**  
  Live compliance scorecards for **ISO 27001 (A.12.6.1)** and **NIST SP 800-53 (RA-5)**, backed by an automated Python ReportLab audit PDF export engine.

---

## Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend** | React 19, Tailwind CSS v4, Vite, Lucide Icons |
| **Backend** | Python 3.11+, FastAPI REST API, SQLAlchemy ORM, Pydantic v2 |
| **Database** | SQLite (`citadel.db`) with 1,000+ realistic synthetic findings |
| **Reporting** | ReportLab PDF Engine |

---

## Quick Start

### 1. Backend & Database Setup
```bash
# Install Python packages
pip install -r backend/requirements.txt

# Seed the database (~1,000 vulnerability findings & audit trails)
python generate_data.py 1000

# Start FastAPI server on port 8000
python -m uvicorn main:app --app-dir backend --host 127.0.0.1 --port 8000 --reload
```

### 2. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

Visit the application at **`http://127.0.0.1:5173/`** (API Docs at `http://127.0.0.1:8000/docs`).
