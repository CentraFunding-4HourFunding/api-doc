# POST /application

Submit files to newly created Lead.

**URL** : 
```
  Production : https://centrafunding.my.salesforce-sites.com/services/apexrest/applicationFiles
  Dev/Test   : https://centrafunding--partial.sandbox.my.salesforce-sites.com/services/apexrest/applicationFiles
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
    "leadId": "String | Required | Lead Id",
    "files": [
        {
            "data": "String | Required | The base64 conversion String of a pdf document",
            "name": "String | Required | The name of the file"
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
    "leadId": "00QWF00000HW0uL2AT",
    "files": [
        {
            "data": "Jvv........",
            "name":"SoS - Altitude Aerial LLC - since 10-10-2022.pdf"
        }
    ],
}
```

## Success Response

**Code** : `201 CREATED`

**Response Body**

```json
{
    "statusCode": "Integer | Status Code",
    "status": "String | The status of the new application"
    "messages" : [
       "String"
    ],
    "id" : "String | Lead ID"
}
```

***Example***

```json
{
    "statusCode": 201,
    "status": "New",
    "messages": [
        "Added File successfully."
    ],
    "id": "00QWF00000HW0uL2AT"
}
```

## Error Response

### If not authorized.

**Code** : `401 UNAUTHORIZED`

### If not data is invalid or missing.

**Code** : `400 Bad Request`

```json
{
  "id": null,
  "messages": [
     "COLLECTION OF ERROR OBJECTS HERE indicating what field is in error and the reason for the error"
  ]
} 
```
