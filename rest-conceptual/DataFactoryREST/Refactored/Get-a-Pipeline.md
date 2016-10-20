---
title: "Get a Pipeline"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-factory
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 81b150cc-d159-40cb-80e1-5660b6d9ac09
caps.latest.revision: 8
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
# Get a Pipeline
  The Get Pipeline operation gets information about the specified pipeline.  
  
## Request  
 The Get Pipeline request may be constructed as follows (HTTPS is recommended):  
  
|**HTTP Verb**|**Request URI**|**HTTP Version**|  
|-|-|-|  
|GET|https://management.azure.com/subscriptions/<SubscriptionID\>/resourcegroups/<ResourceGroupName\>/providers/Microsoft.DataFactory/datafactories/<DataFactoryName\>/datapipelines/<PipelineName\>?api-version=<Api-Version>|HTTP/1.1|  
  
### URI Parameters  
  
|**URI Parameter**|**Required**|**Description**|  
|-|-|-|  
|SubscriptionID|Yes|Your Azure subscription ID.|  
|ResourceGroupName|Yes|A unique name for the resource group that hosts your Azure data factory.|  
|DataFactoryName|Yes|Name for the data factory that you want to find your pipeline.|  
|PipelineName|Yes|Name of pipeline you want to find.|  
|Api-Version|Yes|Specifies the version of the protocol used to make this request.|  
  
### Request Headers  
 The following table describes the request headers.  
  
|Request Header|Required|Description|  
|-|-|-|  
|x-ms-client-request-id|Yes|The operation id for this request.|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
  
-   200 (OK) - if the request was completed successfully.  
  
-   400 (Bad Request) - if the request body fails validation.  
  
-   404 (NotFound) - if the subscription or resource group does not exist.  
  
-   412 (Precondition Failed) - if the condition specified by If-Match header failed.  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|**Response Header**|**Description**|  
|-|-|  
|x-ms-request-id|A unique identifier for the current operation, service generated.|  
|x-ms-ratelimit-remaining-subscription-writes|The remaining limit for current subscription.|  
|x-ms-correlation-request-id|Specifies the tracing correlation Id for the request; the resource provider **must** log this so that end-to-end requests can be correlated across Azure.|  
|x-ms-routing-request-id|Location+DateTime+correlation-request-ID|  
|Date|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 Response body depends on your pipeline property, for more information about pipelines, see [Pipelines and Activities](https://azure.microsoft.com/en-us/documentation/articles/data-factory-create-pipelines/).  
  
```  
  
{  
    "name": <name>,  
    "id": <ID>,  
    "properties": {  
        "description": <description>,  
        "activities": <activity>,  
        "isPaused": <Status>,  
        "provisioningState": <ProvisioningState>,  
        "hubName": <HubName>  
    }  
}  
  
```  
  
 The following table describes the elements of the response body.  
  
|**Element Name**|**Description**|  
|-|-|  
|name|Specifies the name of pipeline.|  
|ID|Specifies the identifying URL of the Pipeline.|  
|Description|Text describing what the activity is used for.|  
|Activity|Activity in the pipeline. A pipeline can have one or more activities.|  
|Status|Specifies whether this pipeline is paused or not|  
|Provisioningstate|Specifies the current provisioning state of the pipeline. When a pipeline is successfully created, the value of the element is **Succeeded**.|  
|Hubname|The hub which contains your pipeline.|  
  
## Sample Request and Response  
 Example URI:  
  
```  
GET: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/adf/providers/Microsoft.DataFactory/datafactories/SPRestDataFactory/datapipelines/ADFTutorialPipeline?api-version=2015-10-01  
```  
  
 The request is sent with the following headers.  
  
```  
x-ms-client-request-id        : 00000000-1111-1111-1111-000000000000  
```  
  
 After the request has been sent, the following response is returned.  
  
 Header:  
  
```  
  
Status Code:  
OK  
  
Headers:  
Pragma                        : no-cache  
x-ms-request-id               : 00000000-1111-1111-1111-000000000000  
x-ms-ratelimit-remaining-subscription-writes: 11999  
x-ms-correlation-request-id   : 00000000-1111-2222-1111-000000000000  
x-ms-routing-request-id       : WESTUS:20141203T213927Z: 00000000-1111-2222-1111-000000000000  
Strict-Transport-Security     : max-age=31536000; includeSubDomains  
Cache-Control                 : no-cache  
Date                          : Wed, 03 Dec 2014 21:39:27 GMT  
Server                        : Microsoft-IIS/8.5  
X-Powered-By                  : ASP.NET  
  
```  
  
 The response includes the following XML body.  
  
```  
  
{  
  "name": "ADFTutorialPipeline",  
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/ADF/providers/Microsoft.DataFactory/datafactories/SPRestDataFactory/datapipelines/ADFTutorialPipeline",  
  "properties": {  
    "description": "Copy data from a blob to Azure SQL table",  
    "activities": [  
      {  
        "type": "Copy",  
        "typeProperties": {  
          "source": {  
            "type": "BlobSource"  
          },  
          "sink": {  
            "type": "SqlSink",  
            "writeBatchSize": 0,  
            "writeBatchTimeout": "00:00:00"  
          }  
        },  
        "inputs": [  
          {  
            "name": "EmpTableFromBlob"  
          }  
        ],  
        "outputs": [  
          {  
            "name": "EmpSQLTable"  
          }  
        ],  
        "policy": {  
          "timeout": "01:00:00",  
          "concurrency": 1,  
          "executionPriorityOrder": "NewestFirst",  
          "style": "StartOfInterval"  
        },  
        "scheduler": {  
          "frequency": "Hour",  
          "interval": 1  
        },  
        "name": "CopyFromBlobToSQL",  
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database"  
      }  
    ],  
    "start": "2015-12-09T00:00:00Z",  
    "end": "2015-12-10T00:00:00Z",  
    "isPaused": false,  
    "runtimeInfo": {  
      "deploymentTime": "2016-02-22T22:40:24.9768561Z",  
      "activePeriodSetTime": "2016-02-22T22:40:25.7707093Z",  
      "activityPeriods": {  
        "copyFromBlobToSQL": {  
          "start": "2015-12-09T00:00:00Z",  
          "end": "2015-12-10T00:00:00Z"  
        }  
      }  
    },  
    "id": "00000000-0000-0000-0000-000000000000",  
    "provisioningState": "Succeeded",  
    "hubName": "sprestdatafactory_hub",  
    "pipelineMode": "Scheduled"  
  }  
}  
  
```  
  
## See Also  
 [Pipelines and Activities in Azure Data Factory](https://azure.microsoft.com/documentation/articles/data-factory-create-pipelines/)  
  
  