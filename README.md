# VisiOCR

## Overview

VisiOCR is an OCR-based web application built using **Python**, **Django**, **OpenCV**, **Tesseract OCR**, and **MySQL**. It extracts information from Aadhaar and PAN cards, validates the extracted data, generates visitor passes with QR codes, and stores visitor information in a database for easy management and retrieval.

---

## Features

### 📤 Image Upload
- Upload Aadhaar or PAN card images for text extraction.
- Validates the uploaded file type and displays an alert for unsupported file formats.

### 🔍 OCR Text Extraction
- Extracts text from uploaded images using **Tesseract OCR**.
- Displays the extracted information on the user interface.
- Generates a unique QR code for every visitor pass.

### 📄 Visitor Pass Generation
- Creates a visitor pass containing the extracted user information and QR code.
- Allows users to download the visitor pass as a PDF.

### ✅ QR Code Validation
- Upload a QR code image to verify whether the visitor pass is **active** or **expired**.
- Displays the visitor pass details if the QR code is valid.

### 💾 Database Storage
- Stores extracted visitor information in a MySQL database for future retrieval and management.

---

## Technologies Used

- Python
- Django
- MySQL
- OpenCV
- Tesseract OCR (pytesseract)
- Regular Expressions (re)
- QRCode
- ReportLab

---

## Installation

### Clone the repository

```bash
git clone https://github.com/sarathvadavalli/VisiOCR-Project
```

### Install dependencies

```bash
pip install opencv-python
pip install pytesseract
pip install regex
pip install qrcode
pip install reportlab
```

### Create Django Project

```bash
django-admin startproject visiOCR
python manage.py startapp visiOCR_app
```

### Configure Database

Update the `DATABASES` configuration in `settings.py`.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'visiocr',
        'USER': 'root',
        'PASSWORD': 'admin',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

### Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### Run the Development Server

```bash
python manage.py runserver
```

---

## Project Workflow

### 1. Upload Image

Users upload an Aadhaar or PAN card image through the web interface.

### 2. Image Preprocessing

The uploaded image is preprocessed using OpenCV techniques such as:
- Grayscale conversion
- Thresholding
- Noise reduction

to improve OCR accuracy.

### 3. Text Extraction

Extract text from the processed image using Tesseract OCR.

```python
import pytesseract

extracted_text = pytesseract.image_to_string(processed_image)
```

### 4. Information Extraction

Regular expressions are used to extract relevant fields such as:
- Name
- Aadhaar Number
- PAN Number
- Date of Birth

from the OCR output.

### 5. QR Code Generation

Generate a QR code containing visitor information with a predefined expiry time.

```python
import qrcode

qr = qrcode.QRCode(
    version=1,
    error_correction=qrcode.constants.ERROR_CORRECT_L,
    box_size=3,
    border=4
)
```

### 6. Visitor Pass Generation

Generate a visitor pass containing:
- Visitor details
- QR Code
- Expiry information

The visitor pass can be downloaded as a PDF.

### 7. QR Validation

Users can upload a QR code to verify whether the visitor pass is still active or has expired.

### 8. Database Storage

All extracted visitor information is stored in a MySQL database for efficient retrieval and management.

---

## Project Structure

```
VisiOCR/
│
├── visiOCR/
├── visiOCR_app/
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── templates/
│   │   ├── home.html
│   │   └── info.html
│   ├── static/
│   │   ├── home.css
│   │   └── info.css
│   └── ...
├── manage.py
└── README.md
```


## Future Enhancements

- Support additional government-issued ID cards.
- Improve OCR accuracy using deep learning models.
- Deploy the application on cloud a platform.

---

## License

This project was developed as part of the **Infosys Springboard Internship Program**.
