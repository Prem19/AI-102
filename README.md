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
             
######################################################################################## 
##  C. Create a Language Understanding solution        

 https://learn.microsoft.com/en-us/training/paths/create-language-solution-azure-cognitive-services/  
       
## Pre-configured features

* Summarization - A summarization query will be sent to an endpoint similar to the following, with the task specified as extractiveSummarizationTasks or ConversationalSummarizationTask

* Named entity recognition - An entity recognition query will be sent to an endpoint similar to the following, with the task specified as EntityRecognition

* Personally identifiable information (PII) detection - A PII query will be sent to an endpoint similar to the following, with the task specified as PiiEntityRecognition.

* Key phrase extraction - KeyPhraseExtraction

* Sentiment analysis - SentimentAnalysis

* Language detection - LanguageDetection

* Conversational language understanding (CLU)

CLU is one of the core custom features offered by Azure Cognitive Services for Language. CLU helps users to build custom natural language understanding models to predict overall intent and extract important information from incoming utterances. CLU does require data to be tagged by the user to teach it how to predict intents and entities accurately.

A language detection query will be sent to an endpoint similar to the following, with the task specified as Conversation. These custom features require extra parameters in the JSON body, including the projectName and deploymentName of your model.

Language Studio - Preview portal at https://language.cognitive.azure.com. 

## REST API 

https://learn.microsoft.com/en-us/training/modules/build-qna-solution-qna-maker/7-consume-qna-client-interfaces

QA: 
```bash
[POST] 
   https://premlanguage.cognitiveservices.azure.com/language/:analyze-conversations?api-version=2022-10-01-preview

Header: 
    Ocp-Apim-Subscription-Key: {*your key}
    Apim-Request-Id: {* your value}

 Request:
   {
      "kind": "Conversation",
      "analysisInput": {
        "conversationItem": {
          "id": "1",
          "text": "What’s the time in Sydney",
          "modality": "text",
          "language": "EN",
          "participantId": "PARTICIPANT_ID_HERE"
        }
      },
      "parameters": {
        "projectName": "Clock",
        "verbose": true,
        "deploymentName": "production",
        "stringIndexType": "TextElement_V8"
      }
    }

Response:
   {
    "kind": "ConversationResult",
      "result": {
        "query": "What’s the time in Sydney",
        "prediction": {
          "topIntent": "GetTime",
          "projectKind": "Conversation",
          "intents": [
            {
              "category": "GetTime",
              "confidenceScore": 0.7823135
            },
            {
              "category": "GetDay'",
              "confidenceScore": 0.6592359
            },
            {
              "category": "None",
              "confidenceScore": 0
            }
          ],
          "entities": [
            
          ]
        }
      }
    }
```

https://microsoftlearning.github.io/AI-102-AIEngineer/Instructions/09b-language-understanding-(preview).html

## Create a Language Service Client Application

## SDK

https://microsoftlearning.github.io/AI-102-AIEngineer/Instructions/10b-language-understanding-client-(preview).html

 ## Import namespaces
 ```bash
 from azure.core.credentials import AzureKeyCredential

 from azure.ai.language.conversations import ConversationAnalysisClient

 from azure.ai.language.conversations.models import ConversationAnalysisOptions
```
## Create a client for the Language service model
  ```bash
 client = ConversationAnalysisClient(
 ls_prediction_endpoint, AzureKeyCredential(ls_prediction_key))
```
## Call the Language service model to get intent and entities
```bash
 convInput = ConversationAnalysisOptions(
     query = userText
     )
    
 cls_project = 'Clock'
 deployment_slot = 'production'

 with client:
     result = client.analyze_conversations(
         convInput, 
         project_name=cls_project, 
         deployment_name=deployment_slot
         )
```
 ## list the prediction results
```bash
 top_intent = result.prediction.top_intent
 entities = result.prediction.entities

 print("view top intent:")
 print("\ttop intent: {}".format(result.prediction.top_intent))
 print("\tcategory: {}".format(result.prediction.intents[0].category))
 print("\tconfidence score: {}\n".format(result.prediction.intents[0].confidence_score))

 print("view entities:")
 for entity in entities:
     print("\tcategory: {}".format(entity.category))
     print("\ttext: {}".format(entity.text))
     print("\tconfidence score: {}".format(entity.confidence_score))

 print("query: {}".format(result.query))
```

       
       
######################################################################################## 
##  D. QA 

https://learn.microsoft.com/en-us/training/paths/build-qna-solution/ 

**Understand question answering** 

https://learn.microsoft.com/en-us/training/modules/build-qna-solution-qna-maker/5-implement-multi-turn-conversation 

## Implement multi-turn conversation
You can enable multi-turn responses when importing questions and answers from an existing web page or document based on its structure, or you can explicitly define follow-up prompts and responses for existing question and answer pairs.

For example, suppose an initial question for a travel booking knowledge base is "How can I cancel a reservation?". A reservation might refer to a hotel or a flight, so a follow-up prompt is required to clarify this detail. The answer might consist of text such as "Cancellation policies depend on the type of reservation" and include follow-up prompts with links to answers about canceling flights and canceling hotels.

When you define a follow-up prompt for multi-turn conversation, you can link to an existing answer in the knowledge base or define a new answer specifically for the follow-up. You can also restrict the linked answer so that it is only ever displayed in the context of the multi-turn conversation initiated by the original question.

## REST API 

https://learn.microsoft.com/en-us/training/modules/build-qna-solution-qna-maker/7-consume-qna-client-interfaces

QA: 
```bash
[POST] 
   https://premlanguage.cognitiveservices.azure.com/language/:query-knowledgebases?projectName=LearnFAQ&api-version=2021-10-01&deploymentName=production 

Header: 
    Ocp-Apim-Subscription-Key: {*your key}

 Request:
   {
  "top": 3,
  "question": "YOUR_QUESTION_HERE",
  "includeUnstructuredSources": true,
  "confidenceScoreThreshold": "YOUR_SCORE_THRESHOLD_HERE",
  "answerSpanRequest": {
    "enable": true,
    "topAnswersWithSpan": 1,
    "confidenceScoreThreshold": "YOUR_SCORE_THRESHOLD_HERE"
  },
  "filters": {
    "metadataFilter": {
      "logicalOperation": "YOUR_LOGICAL_OPERATION_HERE",
      "metadata": [
        {
          "key": "YOUR_ADDITIONAL_PROP_KEY_HERE",
          "value": "YOUR_ADDITIONAL_PROP_VALUE_HERE"
        }
      ]
    }
  }
}

Response:
    {
        "answers": [
            {
                "questions": [
                    "How can I cancel a reservation?"
                ],
                "answer": "Call us on 555 123 4567 to cancel a reservation.",
                "confidenceScore": 1.0,
                "id": 6,
                "source": "https://margies-travel.com/faq",
                "metadata": {},
                "dialog": {
                    "isContextOnly": false,
                    "prompts": []
                }
            }
        ]
    }
```

## Use active learning
Active learning can help you make continuous improvements so that it gets better at answering user questions correctly over time.

Active learning helps improve the knowledge base in two ways:

Implicit feedback: As incoming requests are processed, the service identifies user-provided questions that have multiple, similarly scored matches in the knowledge base. These are automatically clustered as alternate phrase suggestions for the possible answers that you can accept or reject in the Suggestions page for your knowledge base in Language Studio.

Explicit feedback. When developing a client application you can control the number of possible question matches returned for the user's input by specifying the top parameter, as shown here:

https://learn.microsoft.com/en-us/training/modules/build-qna-solution-qna-maker/8-implement-active-learning 



## Define synonyms
```
{
    "synonyms": [
        {
            "alterations": [
                "reservation",
                "booking",,
                ]
        }
    ]
}
```


       
########################################################################################                                                      
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
**------------------------------------------------------------------------------------------------------------------**

**Custom named entity recognition (NER)** 

https://learn.microsoft.com/en-us/training/modules/custom-name-entity-recognition/2-understand-custom-named

## Screenshots

![App Screenshot](https://learn.microsoft.com/en-us/training/wwl-data-ai/custom-name-entity-recognition/media/extraction-development-lifecycle.png#lightbox)

## Considerations for data selection and refining entities

Diversity - use as diverse of a dataset as possible without losing the real-life distribution expected in the real data. You'll want to use sample data from as many sources as possible, each with their own formats and number of entities. It's best to have your dataset represent as many different sources as possible.

Distribution - use the appropriate distribution of document types. A more diverse dataset to train your model will help your model avoid learning incorrect relationships in the data.

Accuracy - use data that is as close to real world data as possible. Fake data works to start the training process, but it likely will differ from real data in ways that can cause your model to not extract correctly.

## How to extract entities
To submit an extraction task, the API requires the JSON body to specify which task to execute. For custom NER, the task for the JSON payload is customEntityRecognitionTasks.

```bash
{
    "displayName": "string",
    "analysisInput": {
        "documents": [
            {
                "id": "doc1", 
                "text": "string"
            },
            {
                "id": "doc2",
                "text": "string"
            }
        ]
    },
    "tasks": {
        "customEntityRecognitionTasks": [      
            {
                "parameters": {
                      "project-name": "myProject",
                      "deployment-name": "myDeployment"
                }
            }
        ]
    }
}

```

## Model Evaluation

Precision : The ratio of successful entity recognitions to all attempted recognitions. A high score means that as long as the entity is recognized, it's labeled correctly.

Recall : The ratio of successful entity recognitions to the actual number of entities in the document. A high score means it finds the entity or entities well, regardless of if it assigns them the right label

F1 score: Combination of precision and recall providing a single scoring metric


## How to interpret metrics
Ideally we want our model to score well in both precision and recall, which means the entity recognition works well. If both metrics have a low score, it means the model is both struggling to recognize entities in the document, and when it does extract that entity, it doesn't assign it the correct label with high confidence.

If precision is low but recall is high, it means that the model recognizes the entity well but doesn't label it as the correct entity type.

If precision is high but recall is low, it means that the model doesn't always recognize the entity, but when the model extracts the entity, the correct label is applied.

########################################################################################     
       

4. Implement knowledge mining solutions 	(5–10%)

       https://learn.microsoft.com/en-us/training/paths/implement-knowledge-mining-azure-cognitive-search/ 


5. Implement conversational AI solutions 	(15–20%)	

       https://learn.microsoft.com/en-us/training/paths/create-conversational-ai-solutions/ 
