
# 🧾 Receipt AI Extractor – Frontend

A React (Vite + TypeScript) web UI that lets you **upload receipt images**, optionally run **client-side OCR** (Tesseract.js/PaddleOCR), and call a backend **REST API** to extract structured receipt details.


## Features Implemented

- Upload receipt images via REST API (`/extract-receipt-details`)
- Receipt data extraction using an open-source OCR engine (Tesseract.js or PaddleOCR)
- Extracted fields: Vendor Name, Date, Currency, Items (Name & Cost), Tax, Total
- Input validation and error handling implemented

## API Endpoints

### POST /extract-receipt-details
Upload a receipt image and extract details.

**Request:**
- Content-Type: multipart/form-data
- Field: `file` (accepts .jpg/.jpeg/.png)

**Response:**
```json
{
  "vendor": "Starbucks",
  "date": "2024-12-10",
  "currency": "GBP",
  "items": [
    {"name": "Latte", "cost": 3.5},
    {"name": "Bagel", "cost": 2.5}
  ],
  "tax": 0.8,
  "total": 6.8
}

-----

🧰 Tech Stack


React + Vite + TypeScript

Axios (API calls)

Tesseract.js / PaddleOCR (optional client-side OCR)

Tailwind CSS or your preferred UI library (optional)


-----

⚙️ Setup

git clone https://github.com/<your-username>/receipt-ai-extractor-frontend.git
cd receipt-ai-extractor-frontend
npm install
cp .env.example .env
npm run dev


.env

VITE_API_BASE_URL=http://localhost:3000
# Toggle client-side OCR in UI if you add it:
VITE_ENABLE_CLIENT_OCR=false

------


# 🧾 Receipt AI Extractor – Monorepo (Frontend + Backend)

A full-stack project for extracting structured data from **receipt images**.

- **Backend (NestJS)**: Accepts image uploads, runs OCR/AI (Tesseract.js), parses fields, persists results, exposes REST.
- **Frontend (React + Vite)**: Uploads receipt images, shows extracted Vendor, Date, Currency, Items, Tax, Total.

## Repos in this monorepo

- `backend/` – NestJS REST API
- `frontend/` – React UI (Vite + TypeScript)

---

## ✨ Features

- Upload receipt images via **POST** `/extract-receipt-details`
- OCR with **Tesseract.js** (or swap for PaddleOCR/Vision API)
- Extracted fields:
  - Vendor, Date, Currency, Items (Name & Cost), Tax, Total
- Input validation + error handling
- Persistence to `uploads/receipts.json` (demo storage)

---

## 🔌 API (backend)

### POST `/extract-receipt-details`
**Request**
- `multipart/form-data` with field `file` (accepts `.jpg/.jpeg/.png`)

**Response**
```json
{
  "vendor": "Starbucks",
  "date": "2024-12-10",
  "currency": "GBP",
  "items": [
    {"name": "Latte", "cost": 3.5},
    {"name": "Bagel", "cost": 2.5}
  ],
  "tax": 0.8,
  "total": 6.8
}
If your backend uses vendor_name instead of vendor, adjust the frontend mapping.


🧰 Local development (without Docker)

Backend

cd backend
cp .env.example .env
npm install
npm run start:dev
# API at http://localhost:3000


Frontend

cd frontend
cp .env.example .env
# set VITE_API_BASE_URL=http://localhost:3000
npm install
npm run dev
# App at http://localhost:5173

------

🧪 Testing

Backend

cd backend
npm run test
npm run test:e2e


(Frontend testing setup is optional; add Vitest/RTL if needed.)

------


🛡️ Notes

uploads/ is generated at runtime (images + receipts.json) and is ignored by git.

Tesseract models are downloaded on first run; the first OCR may be slower.

For production use a real database (PostgreSQL + Prisma/TypeORM), file size limits, rate limiting, and auth.

-----

📄 License

MIT

