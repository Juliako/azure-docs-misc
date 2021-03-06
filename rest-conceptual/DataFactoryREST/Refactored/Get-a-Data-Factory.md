---
title: "Get a Data Factory"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-factory
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3ca4cbbd-7e6c-4bf2-ab51-42d7a56fbd26
caps.latest.revision: 9
author: spelluru
manager: jhubbard
translation.priority.mt: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pt-br
  - ru-ru
  - zh-cn
  - zh-tw
---
# Get a Data Factory
  The Get Data Factory operation gets information about the specified data factory.  
  
## Request  
 The Get Data Factory request may be constructed as follows (HTTPS is recommended):  
  
  
|**HTTP Verb**|**Request URI**|**HTTP Version**|  
|-|-|-|  
|GET|https://management.azure.com/subscriptions/<SubscriptionID\>/resourcegroups/<ResourceGroupName\>/providers/Microsoft.DataFactory/datafactories/<DataFactoryName\>?api-version=<Api-Version>|HTTP/1.1|  
  
### URI Parameters  
  
|**URI Parameter**|**Required**|**Description**|  
|-|-|-|  
|SubscriptionID|Yes|your Azure subscription ID|  
|ResourceGroupName|Yes|The unique name for the resource group that hosts your Azure data factory.|  
|DataFactoryName|Yes|Name of data factory you want to get.|  
|Api-Version|Yes|Specifies the version of the protocol used to make this request.|  
  
### Request Headers  
 The following table describes the request headers.  
  
|**Request Header**|**Required**|**Description**|  
|-|-|-|  
|x-ms-client-request-id|Yes|The operation ID for this request.|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
  
-   200 (OK) - if request was completed successfully.  
  
-   400 (Bad Request) - if request body fails validation.  
  
-   404 (NotFound) - if subscription or resource group does not exist.  
  
-   412 (Precondition Failed) - if condition specified by If-Match header failed.  
  
-   501 (Not Implemented) - if validate is not implemented  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|**Response Header**|**Description**|  
|-|-|  
|x-ms-request-id|A unique identifier for the current operation, service generated.|  
|x-ms-ratelimit-remaining-subscription-writes|The remaining limit for current subscription.|  
|x-ms-correlation-request-id|Specifies the tracing correlation Id for the request; the resource provider **must** log this so that end-to-end requests can be correlated across Azure.|  
|x-ms-routing-request-id|Location+DateTime+correlation-request-ID|  
|Date|A UTC date/time value generated by the service that indicates the time at which the response was initiated|  
  
### Response Body  
  
```  
  
{  
    "name": <Name>  
    "id": <ID>,  
    "type": "Microsoft.DataFactory/datafactories",  
    "location": <location>,  
    "tags": <tag>,  
    "properties": {  
        "dataFactoryId": <DataFactoryID>  
        "hCatalogDescription": null,  
        "provisioningState": <provisioningstate>  
        "error": <Error>,  
        "errorMessage": <ErrorMessage>  
    }  
}  
  
```  
  
 The following table describes the elements of the response body.  
  
|**Element Name**|**Description**|  
|-|-|  
|name|Specifies the name of data factory|  
|id|Specifies the identifying URL of the Data Factory.|  
|location|Specifies the supported Azure location of data factory|  
|tags|A list of key-value pairs that describe the resource|  
|datafactoryID|Auto-generated ID for this data factory.|  
|provisioningstate|Specifies the current provisioning state of the Data Factory. When a Data Factory is successfully created, the value of the element is **Succeeded**|  
|error|Specifies whether any error occurred during deployment.|  
|errormessage|Message related to the error|  
  
## Sample Request and Response  
 Example URI:  
  
```  
GET: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/adf/providers/Microsoft.DataFactory/datafactories/test?api-version=2015-10-01  
```  
  
 The request is sent with the following headers.  
  
```  
x-ms-client-request-id        : 00000000-1111-1111-1111-000000000000  
```  
  
 After the request has been sent, the following response is returned.  
  
```  
  
Status Code:  
OK  
  
Headers:  
Pragma                        : no-cache  
x-ms-request-id               : 00000000-1111-1111-1111-000000000000  
x-ms-ratelimit-remaining-subscription-writes: 799986  
x-ms-correlation-request-id   : 00000000-1111-2222-1111-000000000000  
x-ms-routing-request-id       : WESTUS:20141203T221428Z: 00000000-1111-2222-1111-000000000000  
Strict-Transport-Security     : max-age=31536000; includeSubDomains  
Cache-Control                 : no-cache  
Date                          : Wed, 03 Dec 2014 22:14:27 GMT  
Server                        : Microsoft-IIS/8.5  
X-Powered-By                  : ASP.NET  
  
The response includes the following XML body.  
{  
    "name": "test",  
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/adf/providers/Microsoft.DataFactory/datafactories/test",  
    "type": "Microsoft.DataFactory/datafactories",  
    "location": "westus",  
    "tags": {},  
    "properties": {  
        "dataFactoryId": "00000000-1111-1111-1111-000000000000",  
        "provisioningState": "Succeeded",  
        "error": null,  
        "errorMessage": null  
    }  
}  
  
```  
  
  