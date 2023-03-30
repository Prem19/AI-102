# AI-102 - Study Guide


# 1. Plan and manage an Azure AI solution 	(25–30%)	

https://learn.microsoft.com/en-us/training/paths/prepare-for-ai-engineering/                                                                             https://learn.microsoft.com/en-us/training/paths/provision-manage-azure-cognitive-services/  

 ## Select the appropriate Azure AI service
-> Select the appropriate service for a vision solution

-> Select the appropriate service for a language analysis solution

-> Select the appropriate service for a decision support solution

-> Select the appropriate service in Cognitive Services for a speech solution

-> Select the appropriate Applied AI services

## Plan and configure security for Azure AI services
-> Manage account keys

-> Manage authentication for a resource

-> Secure services by using Azure Virtual Networks

-> Plan for a solution that meets Responsible AI principles

## Create and manage an Azure AI service
-> Create an Azure AI resource

-> Configure diagnostic logging

Manage costs for Azure AI services

Monitor an Azure AI resource

## Deploy Azure AI services
-> Determine a default endpoint for a service

-> Create a resource by using the Azure portal

-> Integrate Azure AI services into a continuous integration/continuous deployment (CI/CD) pipeline

-> Plan a container deployment

-> Implement prebuilt containers in a connected environment

## Create solutions to detect anomalies and improve content
-> Create a solution that uses Anomaly Detector, part of Cognitive Services

-> Create a solution that uses Azure Content Moderator

-> Create a solution that uses Personalizer, part of Cognitive Services

-> Create a solution that uses Azure Metrics Advisor, part of Azure Applied AI Services

-> Create a solution that uses Azure Immersive Reader, part of Azure Applied AI Services

| Feature           | Capability                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Automated machine learning	 | This feature enables non-experts to quickly create an effective machine learning model from data.  |
| Azure Machine Learning designer | A graphical interface enabling no-code development of machine learning solutions.  |
| Data and compute management | Cloud-based data storage and compute resources that professional data scientists can use to run data experiment code at scale. 
| Pipelines	 | Data scientists, software engineers, and IT operations professionals can define pipelines to orchestrate model training, deployment, and management tasks.

## Capabilities of Azure Cognitive Services

**Language**
1. Text analysis	
2. Question answering	
3. Language understanding
4. Translation

**Speech**
1. Speech to Text	
2. Text to Speech	
3. Speech Translation	
4. Speaker Recognition	

**Vision**
1. Image analysis	
2. Video analysis	
3. Image classification	
4. Object detection	
5. Facial analysis	
6. Optical character recognition

**Decision**
1. Anomaly detection
2. Content moderation
3. Content personalization

## Applied AI Services

You can use Cognitive Services to build your own AI solutions, and they also underpin Azure Applied AI Services that provide out-of-the-box solutions for common AI scenarios. Applied AI Services include:

**Azure Form Recognizer** - an optical character recognition (OCR) solution that can extract semantic meaning from forms, such as invoices, receipts, and others.

**Azure Metrics Advisor** - A service build on the Anomaly Detector cognitive service that simplifies real-time monitoring and response to critical metrics.

**Azure Video Analyzer** for Media - A comprehensive video analysts solution build on the Video Indexer cognitive service.

**Azure Immersive Reader** - A reading solution that supports people of all ages and abilities.

**Azure Bot Service** - A cloud service for delivering conversational AI solutions, or bots.

**Azure Cognitive Search** - A cloud-scale search solution that uses cognitive services to extract insights from data and documents.

**------------------------------------------------------------------------------------------------------------------**

## Secure Cognitive Services

**Regenerate keys** 
You should regenerate keys regularly to protect against the risk of keys being shared with or accessed by unauthorized users. You can regenerate keys by using the visual interface in the Azure portal, or by using the az cognitiveservices account keys regenerate Azure command-line interface (CLI) command.

Each cognitive service is provided with two keys, enabling you to regenerate keys without service interruption. To accomplish this:

Configure all production applications to use key 2.
Regenerate key 1
Switch all production applications to use the newly regenerated key 1.
Regenerate key 2.

**------------------------------------------------------------------------------------------------------------------**

## Monitor Cognitive Services costs
To use the pricing calculator to estimate Cognitive Services costs, create a new estimate and select Azure Cognitive Services in the AI + Machine Learning category.

## Manage diagnostic logging

Diagnostic logging enables you to capture rich operational data for a Cognitive Services resource, which can be used to analyze service usage and troubleshoot problems.

**Azure Log Analytics** - a service that enables you to query and visualize log data within the Azure portal.

**Azure Storage** - a cloud-based data store that you can use to store log archives (which can be exported for analysis in other tools as needed).

**------------------------------------------------------------------------------------------------------------------**
## Deploy cognitive services in containers

Containers enable you to host Azure Cognitive Services either on-premises or on Azure. For example, if your application uses sensitive data in an on-premises SQL Server to call a cognitive service, you can deploy Cognitive Services in containers on the same network.

What is a container?

A container comprises an application or service and the runtime components needed to run it, while abstracting the underlying operating system and hardware. In practice, this abstraction results in two significant benefits:

1. Containers are portable across hosts, which may be running different operating systems or use different hardware - making it easier to move an application and all its dependencies.

2. A single container host can support multiple isolated containers, each with its own specific runtime configuration - making it easier to consolidate multiple applications that have different configuration requirement.

A container is encapsulated in a container image that defines the software and configuration it must support. Images can be stored in a central registry, such as Docker Hub, or you can maintain a set of images in your own registry.

## Container deployment

1. A Docker* server.
2. An Azure Container Instance (ACI).
3. An Azure Kubernetes Service (AKS) cluster.

## Use Cognitive Services containers

To deploy and use a Cognitive Services container, the following three activities must occur:

1. The container image for the specific Cognitive Services API you want to use is downloaded and deployed to a container host, such as a local Docker server, an Azure Container Instance (ACI), or Azure Kubernetes Service (AKS).

2. Client applications submit data to the endpoint provided by the containerized service, and retrieve results just as they would from a Cognitive Services cloud resource in Azure.

3. Periodically, usage metrics for the containerized service are sent to a Cognitive Services resource in Azure in order to calculate billing for the service.

![App Screenshot](https://learn.microsoft.com/en-us/training/wwl-data-ai/investigate-container-for-use-cognitive-services/media/cognitive-services-container.png)

| Feature             | Image                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Key Phrase Extraction		 | This feature enables non-experts to quickly create an effective machine learning model from data.|
| Language Detection	 | mcr.microsoft.com/azure-cognitive-services/language|
| Sentiment Analysis v3 (English)	 | mcr.microsoft.com/azure-cognitive-services/sentiment:3.0-en


## Cognitive Services container configuration

When you deploy a Cognitive Services container image to a host, you must specify three settings.

| Setting             | Description                                                                |
| ----------------- | ------------------------------------------------------------------ |
| ApiKey		 | Key from your deployed Azure Cognitive Service; used for billing.|
| Billing	 | Endpoint URI from your deployed Azure Cognitive Service; used for billing.|
| Eula	 | Value of accept to state you accept the license for the container.


https://microsoftlearning.github.io/AI-102-AIEngineer/Instructions/04-use-a-container.html

Note: In this exercise, you’ve deployed the cognitive services container image for text translation to an Azure Container Instances (ACI) resource. You can use a similar approach to deploy it to a Docker host on your own computer or network by running the following command (on a single line) to deploy the language detection container to your local Docker instance, replacing <yourEndpoint> and <yourKey> with your endpoint URI and either of the keys for your cognitive services resource.
```bash
docker run --rm -it -p 5000:5000 --memory 4g --cpus 1 mcr.microsoft.com/azure-cognitive-services/textanalytics/language Eula=accept Billing=<yourEndpoint> ApiKey=<yourKey> 
```
**------------------------------------------------------------------------------------------------------------------**

## What is Anomaly Detector?
Anomaly Detector is an AI service with a set of APIs, which enables you to monitor and detect anomalies in your time series data with little machine learning (ML) knowledge, either batch validation or real-time inference.

https://learn.microsoft.com/en-us/azure/cognitive-services/anomaly-detector/overview 

| Feature             | Description                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Univariate Anomaly Detection		 | This feature enables non-experts to quickly create an effective machine learning model from data.|
| Multivariate Anomaly Detection		| Detect anomalies in multiple variables with correlations, which are usually gathered from equipment or other complex system. The underlying model used is a Graph Attention Network.

## Univariate Anomaly Detection

Enables you to monitor and detect abnormalities in your time series data without having to know machine learning. The algorithms adapt by automatically identifying and applying the best-fitting models to your data, regardless of industry, scenario, or data volume.

| Feature	             | Description                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Streaming detection			 | Detect anomalies in your streaming data by using previously seen data points to determine if your latest one is an anomaly. This operation generates a model using the data points you send, and determines if the target point is an anomaly. By calling the API with each new data point you generate, you can monitor your data as it's created.|
| Batch detection		 | Use your time series to detect any anomalies that might exist throughout your data. This operation generates a model using your entire time series data, with each point analyzed with the same model.|
| Change points detection		 | Use your time series to detect any trend change points that exist in your data. This operation generates a model using your entire time series data, with each point analyzed with the same model.


## Multivariate Anomaly Detection
The Multivariate Anomaly Detection APIs further enable developers by easily integrating advanced AI for detecting anomalies from groups of metrics, without the need for machine learning knowledge or labeled data. Dependencies and inter-correlations between up to 300 different signals are now automatically counted as key factors.


# Anomaly detection modes

https://learn.microsoft.com/en-us/azure/cognitive-services/anomaly-detector/quickstarts/client-libraries?tabs=command-line&pivots=rest-api 


The following request URLs must be combined with the appropriate endpoint for your subscription. For example: 

https://<your-custom-subdomain>.api.cognitive.microsoft.com/anomalydetector/v1.0/timeseries/entire/detect

1. Batch detection

To detect anomalies throughout a batch of data points over a given time range, use the following request URI with your time series data:

/timeseries/entire/detect.

2. Streaming detection

To continuously detect anomalies on streaming data, use the following request URI with your latest data point:

/timeseries/last/detect.

By sending new data points as you generate them, you can monitor your data in real time. A model will be generated with the data points you send, and the API will determine if the latest point in the time series is an anomaly.
 
 **------------------------------------------------------------------------------------------------------------------**
# Azure Content Moderator?

Azure Content Moderator is an AI service that lets you handle content that is potentially offensive, risky, or otherwise undesirable. It includes the AI-powered content moderation service which scans text, image, and videos and applies content flags automatically.

![App Screenshot](
https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/images/content-moderator-mod-api.png)


https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/client-libraries?tabs=visual-studio&pivots=programming-language-rest-api
 
 
 **------------------------------------------------------------------------------------------------------------------**

# Personalizer?

https://learn.microsoft.com/en-us/azure/cognitive-services/personalizer/what-is-personalizer 

Azure Personalizer is an AI service that your applications make smarter decisions at scale using reinforcement learning. Personalizer processes information about the state of your application, scenario, and/or users (contexts), and a set of possible decisions and related attributes (actions) to determine the best decision to make.

Personalizer can determine the best actions to take in a variety of scenarios:

- E-commerce: What product should be shown to customers to maximize the likelihood of a purchase?
- Content recommendation: What article should be shown to increase the click-through rate?
- Content design: Where should an advertisement be placed to optimize user engagement on a website?
- Communication: When and how should a notification be sent to maximize the chance of a response?


https://learn.microsoft.com/en-us/azure/cognitive-services/personalizer/quickstart-personalizer-sdk?pivots=programming-language-python 

## REST API reference 
https://learn.microsoft.com/en-us/rest/api/personalizer/
 
 **------------------------------------------------------------------------------------------------------------------**

## Azure Metrics Advisor?
https://learn.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/overview

Metrics Advisor is a part of Azure Applied AI Services that uses AI to perform data monitoring and anomaly detection in time series data. The service automates the process of applying models to your data, and provides a set of APIs and a web-based workspace for data ingestion, anomaly detection, and diagnostics - without needing to know machine learning.

Use Metrics Advisor to:

- Analyze multi-dimensional data from multiple data sources
- Identify and correlate anomalies
- Configure and fine-tune the anomaly detection model used on your data
- Diagnose anomalies and help with root cause analysis

![App Screenshot](https://learn.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics-advisor-overview.png)
 **------------------------------------------------------------------------------------------------------------------**
 
## Azure Immersive Reader?

https://learn.microsoft.com/en-us/azure/applied-ai-services/immersive-reader/overview 

Immersive Reader is part of Azure Applied AI Services, and is an inclusively designed tool that implements proven techniques to improve reading comprehension for new readers, language learners, and people with learning differences such as dyslexia.

 
######################################################################################## 

# 2. Implement image and video processing solutions 	(15–20%)	

https://learn.microsoft.com/en-us/training/paths/create-computer-vision-solutions-azure-cognitive-services/

https://learn.microsoft.com/en-us/training/paths/extract-text-from-images-documents/ 
       
## Analyze images

-> Select appropriate visual features to meet image processing requirements

-> Create an image processing request to include appropriate image analysis features

-> Interpret image processing responses

## Extract text from images

-> Extract text from images or PDFs by using the Computer Vision service

-> Convert handwritten text by using the Computer Vision service

-> Extract information using prebuilt models in Azure Form Recognizer

-> Build and optimize a custom model for Form Recognizer

## Implement image classification and object detection by using the Custom Vision service, part of Azure Cognitive Services

-> Choose between image classification and object detection models

-> Specify model configuration options, including category, version, and compact

-> Label images

-> Train custom image models, including classifiers and detectors

-> Manage training iterations

-> Evaluate model metrics

-> Publish a trained iteration of a model

-> Export a model to run on a specific target

-> Implement a Custom Vision model as a Docker container

-> Interpret model responses

## Process videos
-> Process a video by using Azure Video Indexer

-> Extract insights from a video or live stream by using Azure Video Indexer

-> Implement content moderation by using Azure Video Indexer

-> Integrate a custom language model into Azure Video Indexer


# Computer Vision resource

- Description and tag generation - determining an appropriate caption for an image, and identifying relevant "tags" that can be used as keywords to indicate its subject.
- Object detection - detecting the presence and location of specific objects within the image.
- Face detection - detecting the presence, location, and features of human faces in the image.
- Image metadata, color, and type analysis - determining the format and size of an image, its dominant color palette, and whether it contains clip art.
- Category identification - identifying an appropriate categorization for the image, and if it contains any known landmarks.
- Brand detection - detecting the presence of any known brands or logos.
- Moderation rating - determine if the image includes any adult or violent content.
- Optical character recognition - reading text in the image.
- Smart thumbnail generation - identifying the main region of interest in the image to create a smaller "thumbnail" version.

```bash
{
  "categories": [
   {
     "name": "_outdoor_mountain",
     "confidence": "0.9"}
  ],
  "adult": {"isAdultContent": "false", …},
  "tags": [
    {"name": "outdoor", "confidence": 0.9},
    {"name": "mountain", " confidence ": 0.9}],
  "description": {
    "tags":["outdoor", "mountain"],
    "captions": [
      {"name": "A mountain with snow",
       "confidence": 0.9
      }
    ]
  },
  "metadata":
    {"width":60,"height":30, format:"Jpeg"},
  "faces": [],
  "brands": [],
  "color": {"dominantColorForeground": "Brown",…},
  "imageType": {"clipArtType": 0, …},
  "objects" : [
    {
     "rectangle": {x:20, y:25, w:10, h:20},
     "object": "mountain",
     "confidence": 0.9
    }
  ]
}
```

```
# Authenticate Computer Vision client
credential = CognitiveServicesCredentials(cog_key) 
cv_client = ComputerVisionClient(cog_endpoint, credential)

```
```
var analysis = await cvClient.AnalyzeImageInStreamAsync(imageData, features);
```

```
# Get image analysis
with open(image_file, mode="rb") as image_data:
    analysis = cv_client.analyze_image_in_stream(image_data , features)

# Get image description
for caption in analysis.description.captions:
    print("Description: '{}' (confidence: {:.2f}%)".format(caption.text, caption.confidence * 100))

# Get image analysis
with open(image_file, mode="rb") as image_data:
    analysis = cv_client.analyze_image_in_stream(image_data , features)

# Get image description
for caption in analysis.description.captions:
    print("Description: '{}' (confidence: {:.2f}%)".format(caption.text, caption.confidence * 100))

# Get image categories
if (len(analysis.categories) > 0):
    print("Categories:")
    landmarks = []
    for category in analysis.categories:
        # Print the category
        print(" -'{}' (confidence: {:.2f}%)".format(category.name, category.score * 100))
        if category.detail:
            # Get landmarks in this category
            if category.detail.landmarks:
                for landmark in category.detail.landmarks:
                    if landmark not in landmarks:
                        landmarks.append(landmark)

    # If there were landmarks, list them
    if len(landmarks) > 0:
        print("Landmarks:")
        for landmark in landmarks:
            print(" -'{}' (confidence: {:.2f}%)".format(landmark.name, landmark.confidence * 100))


# Get brands in the image
if (len(analysis.brands) > 0):
    print("Brands: ")
    for brand in analysis.brands:
        print(" -'{}' (confidence: {:.2f}%)".format(brand.name, brand.confidence * 100))

# Get objects in the image
if len(analysis.objects) > 0:
    print("Objects in image:")

    # Prepare image for drawing
    fig = plt.figure(figsize=(8, 8))
    plt.axis('off')
    image = Image.open(image_file)
    draw = ImageDraw.Draw(image)
    color = 'cyan'
    for detected_object in analysis.objects:
        # Print object name
        print(" -{} (confidence: {:.2f}%)".format(detected_object.object_property, detected_object.confidence * 100))
        
        # Draw object bounding box
        r = detected_object.rectangle
        bounding_box = ((r.x, r.y), (r.x + r.w, r.y + r.h))
        draw.rectangle(bounding_box, outline=color, width=3)
        plt.annotate(detected_object.object_property,(r.x, r.y), backgroundcolor=color)
    # Save annotated image
    plt.imshow(image)
    outputfile = 'objects.jpg'
    fig.savefig(outputfile)
    print('  Results saved in', outputfile)

# Get moderation ratings
ratings = 'Ratings:\n -Adult: {}\n -Racy: {}\n -Gore: {}'.format(analysis.adult.is_adult_content,
                                                                    analysis.adult.is_racy_content,
                                                                    analysis.adult.is_gory_content)
print(ratings)


# Generate a thumbnail
with open(image_file, mode="rb") as image_data:
    # Get thumbnail data
    thumbnail_stream = cv_client.generate_thumbnail_in_stream(100, 100, image_data, True)

# Save thumbnail image
thumbnail_file_name = 'thumbnail.png'
with open(thumbnail_file_name, "wb") as thumbnail_file:
    for chunk in thumbnail_stream:
        thumbnail_file.write(chunk)

print('Thumbnail saved in.', thumbnail_file_name)
```
 **------------------------------------------------------------------------------------------------------------------**

## Analyze video

## Video Analyzer for Media capabilities

- Facial recognition - detecting the presence of individual people in the image. This requires Limited Access approval.
- Optical character recognition - reading text in the video.
- Speech transcription - creating a text transcript of spoken dialog in the video.
- Topics - identification of key topics discussed in the video.
- Sentiment - analysis of how positive or negative segments within the video are.
- Labels - label tags that identify key objects or themes throughout the video.
- Content moderation - detection of adult or violent themes in the video.
- Scene segmentation - a breakdown of the video into its constituent scenes.

https://api.videoindexer.ai.your_endpoint/Videos

```bash
{
  "results": [
    {
      "accountId":  "1234abcd-9876fghi-0156kihb-00123",
      "id":  "a12345bc6",
      "name":  "Responsible AI",
      "description":  "Microsoft Responsible AI video",
      "created":  "2021-01-05T15:33:58.918+00:00",
      "lastModified":  "2021-01-05T15:50:03.123+00:00",
      "lastIndexed":  "2021-01-05T15:34:08.007+00:00",
      "processingProgress":  "100%",
      "durationInSeconds":  114,
      "sourceLanguage":  "en-US",
    }
  ],
}
```
 **------------------------------------------------------------------------------------------------------------------**
 
## Classify Images

The Custom Vision service enables you to build your own computer vision models for image classification or object detection.

To use the Custom Vision service, you must provision two kinds of Azure resource:

A training resource (used to train your models). This can be:
1. **A Cognitive Services resource.**
2. **A Custom Vision (Training) resource.**


A prediction resource, used by client applications to get predictions from your model. This can be:
1. **A Cognitive Services resource.**
2. **A Custom Vision (Prediction) resource.**

 **------------------------------------------------------------------------------------------------------------------**
  
## Detect objects in images

Object detection is used to locate and identify objects in images. You can use Custom Vision to train a model to detect specific classes of object in images.

Object detection is a form of computer vision in which a model is trained to detect the presence and location of one or more classes of object in an image. 

Use the Custom Vision service for object detection
You can use the Custom Vision cognitive service to train an object detection model. To use the Custom Vision service, you must provision two kinds of Azure resource:

A training resource (used to train your models). This can be:
1. **A Cognitive Services resource.**
2. **A Custom Vision (Training) resource.**

A prediction resource, used by client applications to get predictions from your model. This can be:

1. **A Cognitive Services resource.**
2. **A Custom Vision (Prediction) resource.**

 **------------------------------------------------------------------------------------------------------------------**
## Identify options for face detection analysis and identification

![App Screenshot](https://learn.microsoft.com/en-us/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-options.png)


## The Computer Vision service
The Computer Vision service enables you to detect human faces in an image, as well as returning a bounding box for its location.

## The Face service
The Face service offers more comprehensive facial analysis capabilities than the Computer Vision service, including:

- Face detection (with bounding box).
- Comprehensive facial feature analysis (including head pose, presence of spectacles, blur, facial landmarks, occlusion and others).
- Face comparison and verification.
- Facial recognition.

## face service

![App Screesnhot](https://learn.microsoft.com/en-us/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-service.png)

- Face detection - for each detected face, the results include an ID that identifies the face and the bounding box coordinates indicating its location in the image.
- Face attribute analysis - you can return a wide range of facial attributes, including:
    - Head pose (pitch, roll, and yaw orientation in 3D space)
    - Glasses (NoGlasses, ReadingGlasses, Sunglasses, or Swimming Goggles)
    - Blur (low, medium, or high)
    - Exposure (underExposure, goodExposure, or overExposure)
    - Noise (visual noise in the image)
    - Occlusion (objects obscuring the face)
- Facial landmark location - coordinates for key landmarks in relation to facial features (for example, eye corners, pupils, tip of nose, and so on)
- Face comparison - you can compare faces across multiple images for similarity (to find individuals with similar facial features) and verification (to determine that a face in one image is the same person as a face in another image)
- Facial recognition - you can train a model with a collection of faces belonging to specific individuals, and use the model to identify those people in new images.

 **------------------------------------------------------------------------------------------------------------------**



######################################################################################## 

# 3. Implement natural language processing solutions 	(25–30%)	
 
       A. https://learn.microsoft.com/en-us/training/paths/process-translate-text-azure-cognitive-services/ 
       B. https://learn.microsoft.com/en-us/training/paths/process-translate-speech-azure-cognitive-speech-services/   
             
##  Create a Language Understanding solution        

 https://learn.microsoft.com/en-us/training/paths/create-language-solution-azure-cognitive-services/  
       
## Pre-configured features

* Summarization - A summarization query will be sent to an endpoint similar to the following, with the task specified as **extractiveSummarizationTasks** or **ConversationalSummarizationTask**

* Named entity recognition - An entity recognition query will be sent to an endpoint similar to the following, with the task specified as **EntityRecognition**

* Personally identifiable information (PII) detection - A PII query will be sent to an endpoint similar to the following, with the task specified as **PiiEntityRecognition.**

* Key phrase extraction - **KeyPhraseExtraction**

* Sentiment analysis - **SentimentAnalysis**

* Language detection - **LanguageDetection**

* Conversational language understanding (CLU)

CLU is one of the core custom features offered by Azure Cognitive Services for Language. CLU helps users to build custom natural language understanding models to predict overall intent and extract important information from incoming utterances. CLU does require data to be tagged by the user to teach it how to predict intents and entities accurately.

A language detection query will be sent to an endpoint similar to the following, with the task specified as **Conversation**. These custom features require extra parameters in the JSON body, including the projectName and deploymentName of your model.

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


       
## E. Build custom text analytics solutions 
(https://learn.microsoft.com/en-us/training/paths/build-custom-text-analytics/)

**Create custom text classification solutions:** 

## Classification

```bash
Single label classification (json request with **customClassificationTasks**) - you can assign only one class to each file. Following the above example, a video game summary could only be classified as "Adventure" or "Strategy".
Multiple label classification (json request with **customMultiClassificationTasks**) - you can assign multiple classes to each file. This type of project would allow you to classify a video game summary as "Adventure" or "Adventure and Strategy".
```
    
## Screenshots

![App Screenshot](https://learn.microsoft.com/en-us/training/wwl-data-ai/custom-text-classification/media/classify-development-lifecycle.png#lightbox)


## Model Evaluation

**Recall** - Of all the actual labels, how many were identified; the ratio of true positives to all that was labeled.

**Precision** - How many of the predicted labels are correct; the ratio of true positives to all identified positives.

**F1 Score** - A function of recall and precision, intended to provide a single score to maximize for a balance of each component


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
Look for response header with key: **operation-location** - https://premaztextclassify.cognitiveservices.azure.com/text/analytics/v3.2-preview.2/analyze/jobs/ee45db01-9g89-4de8-bbac-3281c6971c1f

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
To submit an extraction task, the API requires the JSON body to specify which task to execute. For custom NER, the task for the JSON payload is **customEntityRecognitionTasks**.

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

**Precision** : The ratio of successful entity recognitions to all attempted recognitions. A high score means that as long as the entity is recognized, it's labeled correctly.

**Recall** : The ratio of successful entity recognitions to the actual number of entities in the document. A high score means it finds the entity or entities well, regardless of if it assigns them the right label

**F1 score**: Combination of precision and recall providing a single scoring metric


## How to interpret metrics
Ideally we want our model to score well in both precision and recall, which means the entity recognition works well. If both metrics have a low score, it means the model is both struggling to recognize entities in the document, and when it does extract that entity, it doesn't assign it the correct label with high confidence.

If precision is low but recall is high, it means that the model recognizes the entity well but doesn't label it as the correct entity type.

If precision is high but recall is low, it means that the model doesn't always recognize the entity, but when the model extracts the entity, the correct label is applied.

########################################################################################     
      
  
# 4. Implement knowledge mining with Azure Cognitive Search(5–10%)

 https://learn.microsoft.com/en-us/training/paths/implement-knowledge-mining-azure-cognitive-search/     
       

## Implement a Cognitive Search solution
-> Provision a Cognitive Search resource

-> Create data sources

-> Define an index

-> Create and run an indexer

-> Query an index, including syntax, sorting, filtering, and wildcards

-> Manage knowledge store projections, including file, object, and table projections

## Apply AI enrichment skills to an indexer pipeline
-> Attach a Cognitive Services account to a skillset

-> Select and include built-in skills for documents

-> Implement custom skills and include them in a skillset

-> Implement incremental enrichment

**------------------------------------------------------------------------------------------------------------------**


## Cognitive Search Solution:

Indexing and querying wide range of data sources. 

## **Skillset**

In Azure Cognitive Search, you can apply artificial intelligence (AI) skills as part of the indexing process to enrich the source data with new information, which can be mapped to index fields. 

The skills used by an indexer are encapsulated in a skillset that defines an enrichment pipeline in which each step enhances the source data with insights obtained by a specific AI skill.

## **Indexer**

The indexer is the engine that drives the overall indexing process. It takes the **outputs extracted using the skills in the skillset, along with the data and metadata values extracted from the original data source, and maps them to fields in the index**.

## **Index**

The index is the searchable result of the indexing process. It consists of a collection of JSON documents, with fields that contain the values extracted during indexing. 

## Apply filtering and sorting
https://learn.microsoft.com/en-us/training/modules/create-azure-cognitive-search-solution/6-apply-filtering-sorting

By including filter criteria in a simple search expression.

By providing an OData filter expression as a $filter parameter with a full syntax search expression.

```
search=London
$filter=author eq 'Reviewer'
queryType=Full
```

## Filtering with facets

Facets are a useful way to present users with filtering criteria based on field values in a result set. They work best when a field has a small number of discrete values that can be displayed as links or options in the user interface.

```
search=*
facet=author
```

## Enhance the index

1. Search-as-you-type (**DocumentsOperationsExtensions.Suggest and DocumentsOperationsExtensions.Autocomplete**)

2. Custom scoring and result boosting
 
  By default, search results are sorted by a relevance score that is calculated based on a term-frequency/inverse-document-frequency (TF/IDF) algorithm.

  You can **customize the way this score is calculated by defining a scoring profile that applies a weighting value to specific fields** - essentially increasing the search score for documents when the search term is found in those fields

**------------------------------------------------------------------------------------------------------------------**

## Create a custom skill for Azure Cognitive Search

You can use the predefined skills in Azure Cognitive Search to greatly enrich an index by extracting additional information from the source data. However, there may be occasions when you have specific data extraction needs that cannot be met with the predefined skills and require some custom functionality.

To support these scenarios, you can implement **custom skills as web-hosted services (such as Azure Functions)**
 that support the required interface for integration into a skillset.
 https://learn.microsoft.com/en-us/training/modules/create-enrichment-pipeline-azure-cognitive-search/9-create-custom-skill 

  Input Schema

```
{
    "values": [
      {
        "recordId": "<unique_identifier>",
        "data":
           {
             "<input1_name>":  "<input1_value>",
             "<input2_name>": "<input2_value>",
             ...
           }
      },
      {
        "recordId": "<unique_identifier>",
        "data":
           {
             "<input1_name>":  "<input1_value>",
             "<input2_name>": "<input2_value>",
             ...
           }
      },
      ...
    ]
}
```

Output Schema

```
{
    "values": [
      {
        "recordId": "<unique_identifier_from_input>",
        "data":
           {
             "<output1_name>":  "<output1_value>",
              ...
           },
         "errors": [...],
         "warnings": [...]
      },
      {
        "recordId": "< unique_identifier_from_input>",
        "data":
           {
             "<output1_name>":  "<output1_value>",
              ...
           },
         "errors": [...],
         "warnings": [...]
      },
      ...
    ]
}
```


## Add a custom skill to a skillset

To integrate a custom skill into your indexing solution, you must add a skill for it to a skillset using the **Custom.WebApiSkill** skill type.

 **"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",**

**------------------------------------------------------------------------------------------------------------------**       

## Knowledge stores

Since the index is essentially a collection of JSON objects, each representing an indexed record, it might be useful to export the objects as JSON files for integration into a data orchestration process using tools such as Azure Data Factory.

You may want to normalize the index records into a relational schema of tables for analysis and reporting with tools such as Microsoft Power BI.

Having extracted embedded images from documents during the indexing process, you might want to save those images as files.

**Azure Cognitive Search supports these scenarios by enabling you to define a knowledge store in the skillset that encapsulates your enrichment pipeline. The knowledge store consists of projections of the enriched data, which can be JSON objects, tables, or image files.** When an indexer runs the pipeline to create or update an index, the projections are generated and persisted in the knowledge store.

## Projections

The projections of data to be stored in your knowledge store are based on the document structures generated by the enrichment pipeline in your indexing process

## Shaper skill
https://learn.microsoft.com/en-us/training/modules/create-knowledge-store-azure-cognitive-search/2-define-projection-json 

To simplify the mapping of these field values to projections in a knowledge store, it's common to use the Shaper skill to create a new, field containing a simpler structure for the fields you want to map to projections.

"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",

## Define a knowledge store
To define the knowledge store and the projections you want to create in it, you must create a **knowledgeStore** object in the skillset that specifies the Azure Storage connection string for the storage account where you want to create projections, and the definitions of the projections themselves.

For object and file projections, the specified container will be created if it does not already exist. An Azure Storage table will be created for each table projection, with the mapped fields and a unique key field with the name specified in the generatedKeyName property.
**------------------------------------------------------------------------------------------------------------------**
## Improve the ranking of a document with term boosting

Azure Cognitive Search lets you query an index using a REST endpoint or inside the Azure portal with the search explorer tool.

## Enable the Lucene Query Parser

1. Boolean operators: **AND, OR, NOT** for example luxury AND 'air con'

2. Fielded search: fieldName:search term for example Description:luxury AND Tags:air con

3. Fuzzy search: **~** for example Description:luxury~ returns results with misspelled versions of luxury

4. Term proximity search: **"term1 term2"~n** for example "indoor swimming pool"~3 returns documents with the words indoor swimming pool within three words of each other

5. Regular expression search: /regular expression/ use a regular expression between / for example /[mh]otel/ would return documents with hotel and motel

6. Wildcard search: *, ? where * will match many characters and ? matches a single character for example 'air con'* would find air con and air conditioning

7. Precedence grouping: (term AND (term OR term)) for example (Description:luxury OR Category:luxury) AND Tags:air?con*

8. Term boosting: **^** for example Description:luxury OR Category:luxury^3 would give hotels with the category luxury a higher score than luxury in the description

       
       
######################################################################################## 

# 5.  Implement conversational AI solutions 	(15–20%)	

https://learn.microsoft.com/en-us/training/paths/create-conversational-ai-solutions/ 
       

## Design and implement conversation flow
-> Design conversational logic for a bot

-> Choose appropriate activity handlers, dialogs or topics, triggers, and state handling for a bot

## Build a conversational bot

-> Create a bot from a template

-> Create a bot from scratch

-> Implement activity handlers, dialogs or topics, and triggers

-> Implement channel-specific logic

-> Implement Adaptive Cards

-> Implement multi-language support in a bot

-> Implement multi-step conversations

-> Manage state for a bot

-> Integrate Cognitive Services into a bot, including question answering, LUIS, and Speech service

## Test, publish, and maintain a conversational bot

-> Test a bot using the Bot Framework Emulator or the Power Virtual Agents web app

-> Test a bot in a channel-specific environment

-> Troubleshoot a conversational bot

-> Deploy bot logic       

**Create conversational AI solutions** 

## Get started with the Bot Framework SDK


**Azure Bot Service** - A cloud service that enables bot delivery through one or more channels, and integration with other services.

**Bot Framework Service** - A component of Azure Bot Service that provides a REST API for handling bot activities.

**Bot Framework SDK** - A set of tools and libraries for end-to-end bot development that abstracts the REST interface, enabling bot development in a range of programming languages.

## Developing a Bot with the Bot Framework SDK

**Empty Bot** - a basic bot skeleton.

**Echo Bot** - a simple "hello world" sample in which the bot responds to messages by echoing the message text back to the user.

**Core Bot** - a more comprehensive bot that includes common bot functionality, such as integration with the Language Understanding service.

Bot application classes and logic
The template bots are based on the Bot class defined in the Bot Framework SDK, which is used to implement the logic in your bot that receives and interprets user input, and responds appropriately. Additionally, bots make use of an Adapter class that handles communication with the user's channel.

Conversations in a bot are composed of activities, which represent events such as a user joining a conversation or a message being received. These activities occur within the context of a turn, a two-way exchange between the user and bot. The Bot Framework Service notifies your bot's adapter when an activity occurs in a channel by calling its Process Activity method, and the adapter creates a context for the turn and calls the bot's Turn Handler method to invoke the appropriate logic for the activity.
QA: 


https://microsoftlearning.github.io/AI-102-AIEngineer/Instructions/13-bot-framework.html 

## Bot application classes and logic

Conversations in a bot are composed of activities, which represent events such as a user joining a conversation or a message being received

These activities occur within the context of a **turn**, a two-way exchange between the user and bot. 

1. **The Bot Framework Service** notifies your bot's adapter when an activity occurs in a channel by calling its **Process Activity** method, 
2. And the adapter creates a context for the turn and calls the bot's **Turn Handler** method to invoke the appropriate logic for the activity.

## Implement activity handlers and dialogs
The logic for processing the activity can be implemented in multiple ways. The Bot Framework SDK provides classes that can help you build bots that manage conversations using:

**Activity handlers:** Event methods that you can override to handle different kinds of activities.

**Dialogs:** More complex patterns for handling stateful, multi-turn conversations.

## 1.Activity handlers
When an activity occurs in a channel, the Bot Framework Service calls the bot adapter's **Process Activity** function, passing the activity details. The adapter creates a **turn context** for the activity and passes it to the bot's turn handler, which calls the individual, event-specific activity handler.

![App Screenshot](https://learn.microsoft.com/en-gb/training/wwl-data-ai/design-bot-conversation-flow/media/activity-handlers.png)

**Turn context**:

An activity occurs within the context of a turn, which represents a single two-way exchange between the user and the bot. Activity handler methods include a parameter for the turn context, which you can use to access relevant information. For example, the activity handler for a message received activity includes the text of the message

## 2.Dialogs
For more complex conversational flows where you need to store state between turns to enable a multi-turn conversation, you can implement dialogs.

1. Component dialogs
2. Adaptive dialogs

## Component dialogs

A component dialog is a dialog that can contain other dialogs, defined in its dialog set. Often, the initial dialog in the component dialog is a **waterfall dialog**, which defines a sequential series of steps to guide the conversation.

![App Screenshot](https://learn.microsoft.com/en-gb/training/wwl-data-ai/design-bot-conversation-flow/media/component-dialog.png)

## Adaptive dialogs
An adaptive dialog is another kind of container dialog in which the flow is more flexible, allowing for **interruptions, cancellations, and context switches** at any point in the conversation. In this style of conversation, the bot initiates a root dialog, which contains a flow of actions (which can include branches and loops), and triggers that can be initiated by actions or by a recognizer


![App Screenshot](https://learn.microsoft.com/en-gb/training/wwl-data-ai/design-bot-conversation-flow/media/adaptive-dialog.png)

**------------------------------------------------------------------------------------------------------------------**


# Understand ways to build a bot

1. Power Virtual Agents
2. Bot Framework Composer
3. Bot Framework SDK

## PVA

Enables users to build a chatbot without requiring any code. PVA lets users use an interface to build conversations, send messages, publish, monitor, and configure your bot all within the PVA app.


## Bot Framework Composer

Bot Framework Composer is an app for developers to build, test, and publish your bot via an interactive interface. Composer is built on the Bot Framework SDK, and supports extending your bot with code for more complex interactions.

## Bot Framework SDK

The Bot Framework SDK is a collection of libraries and tools to build, test, publish, and manage conversational bots. The SDK can connect to other AI services, covers end-to-end bot development, and offers the most authoring flexibility.

## Implementing dialogs with the Bot Framework Composer

One or more actions that define the flow of message activities in the dialog. These include sending a message, prompting the user for input, asking a question, and branching the conversation.


A **Trigger**, which invokes the dialog logic for certain conditions or based on intent detected.

A **recognizer**, which interprets user input to determine semantic intent. Recognizers are based on the Language Understanding service by default, but you can also use other types of recognizer; such as the QnA Service or simple regular expression matches.


In addition to these elements, a dialog has memory in which values are stored as properties. **Properties** can be defined at various scopes, including the user scope (variables that store information for the lifetime of the user session with the bot, such as user.greeted) and dialog scope (variables that persist for the lifetime of the dialog, such as dialog.response).
