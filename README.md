# pdf-service
Micro Service endpoint to fill and extract data from a pdf form

# Registration
To register for token select link below to access registration page. After filling out your information you will 
receive an email to the address you provided.
## 
https://services.airspringsoftware.com/tokenservice

![Registration Page](https://github.com/airspringsoftware/pdf-service/blob/master/Screen%20Shot%202017-08-25%20at%209.15.56%20AM.png)

# API

## /fill

Pass in token you received when you registered.
https://services.airspringsoftware.com/forms/api/fill.json

### Parameters
```sh
"token": "3972b8cccc77ad0abfc5b5e0",
"file": "https://www.irs.gov/pub/irs-pdf/fw4.pdf",
"formData": {
  "topmostSubform[0].Page1[0].Line1[0].f1_09_0_[0]":"Ronald",
  "topmostSubform[0].Page1[0].Line1[0].f1_10_0_[0]": "Heiney"
}
```

### Response
```sh
{
    "response": {
        "pdfComplete": true,
        "pdfRoute": "/output/pdf/fw4-4439cdd7001b895fff43c52f-5a15fd9ebfb28b2e33210e6b.pdf"
    }
}
``` 
To get the filled pdf file 
https://services.airspringsoftware.com/output/pdf/fw4-4439cdd7001b895fff43c52f-5a15fd9ebfb28b2e33210e6b.pdf

## /extract

Pass in token you received when you registered.
https://services.airspringsoftware.com/forms/api/extract.json

### Parameters
```sh
token=3972b8cccc77ad0abfc5b5e0
file=https://github.com/airspringsoftware/pdf-service/blob/master/fw4-filled.pdf?raw=true
```  

### Response
```sh
{
    "response": {
        "formInfo": {
            "AcroForm": true,
            "XFA": true,
            "needsRendering": false,
            "numFields": 42
        },
        "fields": [
            {
                "index": 0,
                "type": "Text",
                "name": "topmostSubform[0].Page1[0].f1_01_0_[0]",
                "value": null,
                "options": []
            },
            {
                "index": 1,
                "type": "Text",
                "name": "topmostSubform[0].Page1[0].f1_02_0_[0]",
                "value": null,
                "options": []
            },
``` 

# Samples

## Fill
```sh
curl -X POST \
  https://services.airspringsoftware.com/forms/api/fill.json \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{ 
  "token": "b4ae47e50536ba055ae4134d",
  "file": "https://www.irs.gov/pub/irs-pdf/fw4.pdf",
  "formData": {"topmostSubform[0].Page1[0].Line1[0].f1_09_0_[0]": "Ronald","topmostSubform[0].Page1[0].Line1[0].f1_10_0_[0]": "Heiney"}}'
```
## Extract
```sh
curl -X GET \
  'https://services.airspringsoftware.com:6001/forms/api/extract.json?token=3972b8cccc77ad0abfc5b5e0&file=https%3A%2F%2Fgithub.com%2Fairspringsoftware%2Fpdf-service%2Fblob%2Fmaster%2Ffw4-filled.pdf%3Fraw%3Dtrue' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

