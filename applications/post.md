# POST /application

Submit a new credit application to Centra Platform.

**URL** : 
```
  Production : https://
  Dev/Test   : https://centrafunding--partial.sandbox.my.salesforce-sites.com/services/apexrest/application
```


**Method** : `POST`

**Request Headers**

| Name | Value |
|:-----|:------|
|Accept|application/json|

**Request Body**

```json
{
    "authorizationCode": "String | Required | An identifier that can be set to correlate applications with entities.",
    "partnerRepEmail": "Boolean | Optional | Email Address of Sales person",
    "transactionSummary": "String | Optional | Transaction notes.",
    "isCorpOnly": "Boolean | Required | True/False",

    "borrower": {
        "name": "String | Required | The name of the company",
        "dba": "String | Optional | The DBA of the company",
        "address": {
            "street": "String | Required | The company headquarters street address",
            "city": "String | Required | The city where the company headquarters is located ",
            "state": "String | Required | The state/prov where the company headquarters is located",
            "zip": "String | Required | The zip/postal of the company headquarters",
         },
        "phone": "String | Optional | The phone Number for the company headquarters",
        "businessEntityType" : "String | Optional | Sole-Proprietorship, Partnership, LLC, Corporation",
        "federalTaxIdNumber" : "String | Optional | The EIN# issued to the company by the IRS. Example",
        "establishedDate" : "String | Optional | Date format YYYY-MM-DD",
        "businessDescription" : "String | Optional | Example: Automotive Business, Mechanic, Doctor, Restaurant, Car Wash, Trucking, Construction, Landscaping, etc.",
        "website" : "String | Optional | URL for borrower’s website",
        "email": "String | Optional | The guarantor's phone Number"
    },

    "guarantors": [
        {
            "isGuarantor" : "Boolean | Required | True/False",
            "firstName": "String | Required | The guarantor's first name",
            "lastName": "String | Required | The guarantor's last name",
            "title": "String | Optional | Title of the Guarantor",
            "address": {
               "street": "String | Optional | The guarantor's street address",
               "city": "String | Optional | The city",
               "state": "String | Optional | The state/prov",
               "zip": "String | Optional | The zip/postal",
            },
            "email": "String | Optional | The guarantor's phone Number",
            "phone": "String | Optional | The guarantor's phone Number",
            "ssn": "String | Optional | The guarantor's Social Security Number",
            "percentOfOwnership": "Number | Optional | The percentage owned",
            "authorizedCreditRelease": "Boolean | Optional | Authorization for credit release.",
            "isHomeOwner" : "Boolean | Optional | True/False"
    	}
    ],

    "equipments": [
        {
            "description": "String | Required | The product description",
            "price": "Number | Required | The product price"
            "condition": "String | Required | The condition of the equipment - 'new' | 'used'",
            "address": {
               "street": "String | Optional | The equipment location street address",
               "city": "String | Optional | The city",
               "state": "String | Optional | The state/prov",
               "zip": "String | Optional | The zip/postal",
            },
            "vendorName": "String | Optional | The vendor's name",
            "vendorAddress": {
               "street": "String | Optional | The equipment vendor street address",
               "city": "String | Optional | The city",
               "state": "String | Optional | The state/prov",
               "zip": "String | Optional |  The zip/postal",
            },
            "vendorPhone": "String | Optional |  The vendors's phone",
        }
    ],

    "files": [
        {
            "stream": "String | Optional | The base64 conversion String of a pdf document",
            "name": "String | Optional |  The name of the file"
        }
    ],

}
```

***Links***

***Example - Full Credit Application***

A "full" credit application contains all information necessary to receive instant financing quotes. The guarantors you list will not be required to provide any additional information when you use this submission method.

```json
{
    "authorizationCode": "a0936dc61bd065036e6e81ef56a3fe87",
    "partnerRepEmail": "mypartneremail@partner.com",
    "borrower": {
        "name": "Test Company Name",
        "dba" : "Test Inc",
        "address" : {
            "street": "123 Main St",
            "city": "Minneapolis", 
            "state": "MN", 
            "zip": "55401"
        },
        "phone": "555-555-5555",
        "establishedDate": "2011-10-25"
    },
    "guarantors" : [
        {
            "firstName": "John",
            "lastName": "Doe",
            "address" : {
                "street":"123 Oklahoma Ave",
                "city" : "Oklahoma City",
                "state": "OH",
                "zip":"22222"
            },
            "phone": "111-222-3333",
            "ssn": "111-11-1111",
            "percentOfOwnership": 100.00,
            "authorizedCreditRelease": true
        }
    ],
    "equipments" : [
        {
            "description": "desc",
            "price": 10000.00,
            "condition": "New",
            "address" : {
                "street":"123 Oklahoma Ave",
                "city" : "Oklahoma City",
                "state": "OH",
                "zip":"22222"
            },
            "vendorName"  : null,
            "vendorAddress" : null,
            "vendorPhone" : null
        }
    ],
}
```

## Success Response

**Code** : `201 CREATED`

**Response Body**

```json
{
    "id": "String | The id of the new application",
    "status": "String | The status of the new application"
}
```

***Example***

```json
{
    "id": "000000000000",
    "status": "New"
}
```

## Error Response

### If not authorized.

**Code** : `401 UNAUTHORIZED`

### If not data is invalid or missing.

**Code** : `400 Bad Request`

```json
{
  "id": null | "",
  "message": "Data Validation Errors, please correct and try again",
  "errors": [
    {
      "message": "COLLECTION OF ERROR OBJECTS HERE indicating what field is in error and the reason for the error"
    }
  ]
} 
```
