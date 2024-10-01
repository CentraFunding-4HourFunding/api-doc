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
    "authorizationCode": "string | Required | An identifier that can be set to correlate applications with entities.",
    "partnerRepEmail": "boolean | Optional | Email Address of Sales person",

    "borrower": {
        "name": "string | The name of the company",
        "address": {
            "street": "string | The company headquarters street address",
            "city": "string | The city where the company headquarters is located ",
            "state": "string | The state/prov where the company headquarters is located",
            "zip": "string | The zip/postal of the company headquarters",
         },
        "phone": "string | The phone number for the company headquarters",
        "establishedDate" : "string | Date format YYYY-MM-DD"
    },

    "guarantors": [
        {
            "firstname": "string | The guarantor's first name",
            "lastname": "string | The guarantor's last name",
            "address": {
               "street": "string | The guarantor's street address",
               "city": "string | The city",
               "state": "string | The state/prov",
               "zip": "string | The zip/postal",
            },
            "phone": "string | The guarantor's phone number",
            "ssn": "string | The guarantor's Social Security Number",
            "percentofOwnership": "number | The percentage owned",
            "authorizedCreditRelease": "boolean | Authorization for credit release.",
    	}
    ],

    "equipments": [
        {
            "description": "string | The product description",
            "price": "number | The product price"
            "condition": "string | The condition of the equipment - 'new' | 'used'",
            "address": {
               "street": "string | The equipment location street address",
               "city": "string | The city",
               "state": "string | The state/prov",
               "zip": "string | The zip/postal",
            },
            "vendorName": "string | The vendor's name",
            "vendorAddress": {
               "street": "string | The equipment vendor street address",
               "city": "string | The city",
               "state": "string | The state/prov",
               "zip": "string | The zip/postal",
            },
            "vendorPhone": "string | The vendors's phone",
        }
    ],

    "files": [
        {
            "stream": "string | The base64 conversion string of a pdf document",
            "name": "string | The name of the file"
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
            "firstname": "John",
            "lastname": "Doe",
            "address" : {
                "street":"123 Oklahoma Ave",
                "city" : "Oklahoma City",
                "state": "OH",
                "zip":"22222"
            },
            "phone": "111-222-3333",
            "ssn": "111-11-1111",
            "percentofOwnership": 100.00,
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
    "application_id": "string | The id of the new application",
    "status": "string | The status of the new application"
}
```

***Example***

```json
{
    "app_id": "000000000000",
    "status": "New"
}
```

## Error Response

### If not authorized.

**Code** : `401 UNAUTHORIZED`
