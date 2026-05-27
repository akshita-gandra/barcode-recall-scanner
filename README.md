# Barcode Recall Scanner — AI-Powered Food Recall & Ingredient Risk App

> **UC Berkeley MIDS W210 Capstone** · Spring 2026
> Team project with capstone teammates. Original product concept by Akshita Gandra. This repo is my copy of the team codebase, maintained for portfolio purposes.

A mobile-friendly web app that lets consumers scan grocery barcodes or receipt photos to instantly check for active FDA food recalls and assess ingredient-level health risk against personalized allergen and dietary profiles.

🔗 [Berkeley I-School project page](https://www.ischool.berkeley.edu/projects/2026/safe-cart-real-time-food-safety-intelligence)
🔗 [Product Demo] (https://vimeo.com/1182072357?fl=pl&fe=sh)

---

## Why This Exists

Roughly 48 million Americans get sick from foodborne illness every year. The FDA issues hundreds of food recalls annually, but discovery is fragmented across press releases, retailer notices, and news headlines — by the time most consumers learn about a recall, the product is already in their pantry. This app collapses that gap into a single barcode scan.

---

## What It Does

- **Barcode scan** → check the product against the openFDA enforcement feed in real time
- **Receipt photo upload** → OCR every line item via AWS Textract and check each one
- **Personalized risk scoring** → match ingredient lists against user allergen and dietary profiles
- **Saved grocery lists** → email alerts when something you've bought enters a recall window

---

## Tech Stack

| Layer | Tech |
|---|---|
| Backend | FastAPI · gunicorn (uvicorn workers) |
| Frontend | React · TypeScript · Vite · Tailwind |
| Database | PostgreSQL on AWS RDS |
| OCR | AWS Textract |
| LLM | Claude Haiku via AWS Bedrock (ingredient disambiguation) |
| Product data | Open Food Facts API with RDS cache |
| Recall data | openFDA enforcement API (refreshed every 6 hrs) |
| Infrastructure | AWS EC2 (Ubuntu) · nginx · S3 · SES · IAM |

---

## My Contributions

- Originated the product concept and led the problem framing for the capstone team
- Designed the ingredient risk-scoring logic combining synonym normalization, fuzzy matching (RapidFuzz), TF-IDF cosine similarity, and cross-encoder reranking
- Integrated Claude Haiku (Bedrock) for LLM-based ingredient disambiguation on edge cases the deterministic pipeline couldn't resolve
- Drove the user-facing risk communication design — how raw model outputs translate into clear, actionable consumer guidance
- Contributed to AWS infrastructure work (RDS, IAM, SES alerting)

---

## Repo Structure

```
.
├── backend/        FastAPI app (app.py, database.py, recall_update.py, receipt_scan.py)
├── frontend/       React + TypeScript (Vite) — mobile-first UI
└── misc/           Architecture docs, DB setup scripts, sample data
```

---

## Local Development

### Backend
```bash
cd backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env   # fill in DB creds
uvicorn app:app --reload
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```
