# filter-script


wardpdf (folder)->

  ward.py --- demo logic for filtering using PyMuPDF, OCR-pytesseract
FastAPI (folder)--> for web install requirment.txt



    # filter-script
🗳️ WardPDF – Voter List Filtering System

WardPDF is a tool for filtering voter list PDFs by house number using:

PyMuPDF for rectangle detection (from PDF drawings)

pytesseract for Malayalam + English OCR

FastAPI for a simple web API interface

📁 Project Structure
wardpdf/
│
├── ward.py                  # Local demo script for direct filtering
│
└── fastapi/                 # Web version (FastAPI app)
    ├── app.py               # FastAPI entrypoint (main server)
    ├── requirements.txt     # Dependencies for web setup
    └── voter_filter/
        ├── __init__.py
        ├── core.py          # Main filtering logic
        ├── helper.py        # OCR + rectangle helper functions
        └── settings.py      # Configuration constants

⚙️ Requirements

Python ≥ 3.9

Tesseract OCR installed and available in PATH

Windows: UB Mannheim build

Linux/macOS:

sudo apt install tesseract-ocr tesseract-ocr-mal


Malayalam OCR file (mal.traineddata) must exist in:

C:\Program Files\Tesseract-OCR\tessdata\

🧰 Installation

Navigate to the FastAPI folder:

cd wardpdf/fastapi


Install dependencies:

pip install -r requirements.txt


requirements.txt

fastapi
uvicorn
PyMuPDF
pillow
pytesseract
numpy
python-multipart

🧪 Running Locally (Web API)

Start the FastAPI server:

uvicorn app:app --reload


Open your browser at:
👉 http://127.0.0.1:8000/docs

Under /filter, click “Try it out”:

Upload your voter list PDF (e.g. ward 17.pdf)

Enter a house number (e.g. 15/350)

Click Execute

The response will be a filtered PDF containing only matching voter boxes.

🧩 API Endpoint
POST /filter

Request

Field	Type	Description
file	multipart/form-data	PDF file upload
house_no	string	House number to filter (e.g. 15/350)

Response

200: PDF file with filtered boxes

404/500: Error message (if no match or internal error)

Example (using curl):

curl -X POST "http://127.0.0.1:8000/filter" \
  -F "house_no=4/54" \
  -F "file=@ward 17.pdf;type=application/pdf" \
  -o filtered_output.pdf

🧮 Running Locally (Script Mode)

If you only want to test the core logic without the web API:

From inside wardpdf/:

python ward.py


It will:

Ask for a house number

Filter the PDF

Produce filtered_output.pdf locally

⚡ Notes

Default OCR region: left half of each voter box (for faster recognition).

Output layout: 2 × 20 grid per page with full-box crops.

Adjust DPI and layout in settings.py if needed for quality or speed.

📦 Deliverable Summary for Developer
Folder/File	Purpose
ward.py	Local demo script for reference
fastapi/app.py	FastAPI web entrypoint
fastapi/requirements.txt	Web dependencies
fastapi/voter_filter/core.py	Filtering logic
fastapi/voter_filter/helper.py	OCR + geometry helpers
fastapi/voter_filter/settings.py	Constants and config
