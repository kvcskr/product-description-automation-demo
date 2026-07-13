# n8n — Automated Product Description Generator

An n8n workflow that automatically generates ready-to-publish product descriptions from product photos using GPT-4.1 Vision. Results are saved directly to Google Sheets the moment a new product folder appears in Google Drive.

---

## The Problem It Solves

Writing product descriptions manually is time-consuming — someone reviews photos, writes the copy, formats features and benefits, then enters everything into a spreadsheet. With dozens or hundreds of products, this takes hours every week.

This workflow automates the entire process. Upload product photos to a Google Drive folder — structured descriptions appear in the spreadsheet automatically within minutes, without any manual action.

---

## How It Works

```
New product folder added to Google Drive
        ↓
n8n detects the new folder (polling every minute)
        ↓
Download all photos from the folder (multiple angles)
        ↓
GPT-4.1 Vision — analyze photos and generate description
        ↓
Parse AI response (name, brand, description, features, EAN)
        ↓
Append ready row to Google Sheets
```

**Google Drive folder structure:**
```
Product Photos/
  Product A/
    photo1.jpg
    photo2.jpg
  Product B/
    photo1.jpg
```

Each subfolder = one product. Drop 5 folders at once — the workflow processes each one automatically in a separate execution.

---

## What GPT-4.1 Generates

| Field | Description |
|-------|-------------|
| Product name | Full name with weight or size if visible |
| Brand | Manufacturer name |
| Short description | 3 sentences in a professional tone |
| Features & benefits | 2–4 lines in `feature – benefit` format |
| EAN barcode | If visible in the photo |

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Automation | n8n |
| AI Vision | GPT-4.1 (OpenAI) |
| Trigger | Google Drive (folder watch) |
| Photo storage | Google Drive |
| Output | Google Sheets |

---

## Setup

1. Download `workflow_automatyzacja_opisow.json`
2. In n8n: **Import from file** → upload the JSON
3. Add your credentials: OpenAI API, Google Drive OAuth, Google Sheets OAuth
4. Replace the following placeholders in the workflow:

| Placeholder | Where to find it |
|-------------|-----------------|
| `TWOJE_FOLDER_ID_GOOGLE_DRIVE` | Drive URL: `/folders/YOUR_ID` |
| `TWOJE_SPREADSHEET_ID` | Sheets URL: `/d/YOUR_ID/` |

5. Activate the workflow — it runs continuously and processes new product folders automatically
