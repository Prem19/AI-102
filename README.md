# AI-102 - Study Guide, PostMan Collections for cognitive services, SDK(Python)

 Designing and Implementing a Microsoft Azure AI Solution 

1. Plan and manage an Azure AI solution 	(25–30%)	

       https://learn.microsoft.com/en-us/training/pathsprepare-for-ai-engineering/

       https://learn.microsoft.com/en-us/training/paths/provision-manage-azure-cognitive-services/ 


2. Implement image and video processing solutions 	(15–20%)	

       https://learn.microsoft.com/en-us/training/paths/create-computer-vision-solutions-azure-cognitive-services/

       https://learn.microsoft.com/en-us/training/paths/extract-text-from-images-documents/ 


3. Implement natural language processing solutions 	(25–30%)	
 
       A. https://learn.microsoft.com/en-us/training/paths/process-translate-text-azure-cognitive-services/ 
       B. https://learn.microsoft.com/en-us/training/paths/process-translate-speech-azure-cognitive-speech-services/   
       C. https://learn.microsoft.com/en-us/training/paths/create-language-solution-azure-cognitive-services/  
       D. https://learn.microsoft.com/en-us/training/paths/build-qna-solution/ 
       
       

## E. Build custom text analytics solutions 
(https://learn.microsoft.com/en-us/training/paths/build-custom-text-analytics/)

**Create custom text classification solutions:** 

## Classification

```bash
Single label classification (json request with customClassificationTasks) - you can assign only one class to each file. Following the above example, a video game summary could only be classified as "Adventure" or "Strategy".
Multiple label classification (json request with customMultiClassificationTasks) - you can assign multiple classes to each file. This type of project would allow you to classify a video game summary as "Adventure" or "Adventure and Strategy".
```
    
## Screenshots

![App Screenshot](https://learn.microsoft.com/en-us/training/wwl-data-ai/custom-text-classification/media/classify-development-lifecycle.png#lightbox)


## Model Evaluation

Recall - Of all the actual labels, how many were identified; the ratio of true positives to all that was labeled.

Precision - How many of the predicted labels are correct; the ratio of true positives to all identified positives.

F1 Score - A function of recall and precision, intended to provide a single score to maximize for a balance of each component


## REST API 

https://learn.microsoft.com/en-us/training/modules/custom-text-classification/3-understand-how-to-build-projects

1. Consuming Deployed model: 
```bash
[POST] 
    https://premaztextclassify.cognitiveservices.azure.com/text/analytics/v3.2-preview.2/analyze

Header: 
    Ocp-Apim-Subscription-Key: {*your key}

 Request:
    {
    "displayName": "myJob",
    "analysisInput": {
        "documents": [
        {
            "id": "doc1",
            "text": "Text for document 1"
        },
        {
            "id": "doc2",
            "text": "Text for document 2"
        }
        ]
    },
    "displayName": "myClassification",
    "tasks": {
        "customClassificationTasks": [
        {
            "parameters": {
            "project-name": "*ClassifyLab",
            "deployment-name": "*artices"
            }
        }
        ]
    }
    } 
```

Response: (202)
Look for response header with key: operation-location - https://premaztextclassify.cognitiveservices.azure.com/text/analytics/v3.2-preview.2/analyze/jobs/ee45db01-9g89-4de8-bbac-3281c6971c1f

2. Get the classification results:

```bash
  
[GET] 
    https://premaztextclassify.cognitiveservices.azure.com/text/analytics/v3.2-preview.2/analyze/jobs/ee45db01-9g89-4de8-bbac-3281c6971c1f

Header: 
    Ocp-Apim-Subscription-Key: {* your value}

 Response:
    {
        "jobId": "0e8ddcfe-b081-4d26-8010-ca4a4d5c7e1c",
        "lastUpdateDateTime": "2023-03-25T11:07:19Z",
        "createdDateTime": "2023-03-25T11:07:18Z",
        "expirationDateTime": "2023-03-26T11:07:18Z",
        "status": "succeeded",
        "errors": [],
        "displayName": "myClassification",
        "tasks": {
            "completed": 1,
            "failed": 0,
            "inProgress": 0,
            "total": 1,
            "customSingleClassificationTasks": [
                {
                    "lastUpdateDateTime": "2023-03-25T11:07:19.7010658Z",
                    "state": "succeeded",
                    "results": {
                        "documents": [
                            {
                                "id": "doc1",
                                "classification": {
                                    "category": "Entertainment",
                                    "confidenceScore": 0.26
                                },
                                "warnings": []
                            },
                            {
                                "id": "doc2",
                                "classification": {
                                    "category": "Entertainment",
                                    "confidenceScore": 0.26
                                },
                                "warnings": []
                            }
                        ],
                        "errors": [],
                        "projectName": "ClassifyLab",   {* your value}
                        "deploymentName": "artices"     {* your value}
                    }
                }
            ]
        }
    }

```
       

4. Implement knowledge mining solutions 	(5–10%)

       https://learn.microsoft.com/en-us/training/paths/implement-knowledge-mining-azure-cognitive-search/ 


5. Implement conversational AI solutions 	(15–20%)	

       https://learn.microsoft.com/en-us/training/paths/create-conversational-ai-solutions/ 
