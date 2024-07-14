# VisiOCR
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;OCR stands for Optical character recognition. VisiOCR is an application which is used to extract and validate the text from aadhaar or pan cards and generate a visitor pass along with a QR-code for the user with a fixed duration. This data can be conviniently stored in database for easy storage and retrieval.

## Features
<b>a) Upload image:</b> The user can select the type of image he/she wants to scan and upload the image. If the extension of uploaded file doesnot match with that of image, it shows an alert to the user.<br>

<b>b) Extract text:</b> After user uploads an image, the text is extracted from image using pytesseract library and a QR-code is generated. All these details are displayed on the user interface.

<b>c) Download pdf:</b> When user clicks on download as pdf button, it is downloaded in the pdf format and stored in local disk.

## Steps Followed
* Clone the repository using git clone command.
```
git clone https://github.com/Springboard-Internship-2024/VisiOCR_May_2024.git
```
* Install the necessary libraries needed for project.
```
pip install opencv-python
pip install pytesseract
pip install regex
pip install qrcode
pip install reportlab
```
* Create a <b>Django</b> project visiOCR and an app named visiOCR_app.
```
django-admin startproject visiOCR
python manage.py startapp visiOCR_app
```
* Update the settings by adding the app name and paths for templates and static files. Also create a connection to MySQL server by giving required details of database.
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'visiocr',
        'USER': 'root',
        'PASSWORD': 'admin',
        'HOST':'localhost',
        'PORT':'3306',
    }
}
```
* Create home.html and info.html templates. Also home.css and info.css for styling respective pages.
  - home.html to enable user to upload an image for extraction.
  - info.html to display the extracted details along with QR-code.
 
* Create a model visiOCR_data and add fields into it. Then apply migrations and migrate to see the changes in database.
```
class OCR_data(models.Model):
    pass_id = models.AutoField(primary_key=True)
    id_type = models.CharField(max_length=20)
    text = models.CharField(max_length=100)
```
    
* Preprocess the image and Extract the data from uploaded image using <b>pytesseract</b> library.
```
import pytesseract
extracted_text = pytesseract.image_to_string(processed)
```
* Fetch the required details from extracted text using regular expressions which can be achieved by re module.
* Generate a QR-code which stores these details and has a fixed expiry time after which the code becomes invalid. Before expiry, when this QR is scanned in a mobile, the details are visible.
```
import qrcode
qr = qrcode.QRCode(version=1, error_correction=qrcode.constants.ERROR_CORRECT_L, box_size=3, border=4)
```
* Generate a visitor pass which contains all the extracted details along with QR code. Download the page once download button is clicked.
* The visitor pass details are then pushed and stored into MySQL database.
