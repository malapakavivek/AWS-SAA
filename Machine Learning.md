- - - 
### Amazon Rekognition 

- Facial analysis and search 
	- user verification
	- people count 
- find objects, people in images 

- create database of familiar faces 

- Use case:
	- object labelling
	- language recognition (on an image)
	- face search
	- face analysis (gender, age range, emotion)

**Content Moderation**
- detect nsfw content
- used in social media, broadcast, e-commers for safe user experience
- set a confidence level and match your raw data with the confidence level - more confidence -> flag that item
- optional human manual review

![[Pasted image 20240923234001.png|150]]

---
### Amazon Transcribe 

- automatically converts speech to text
- uses deep learning process called Automatic Speech Recognition (SRS) for the conversion 
- automatically remove personal identifiable information 
- can recognize languages in audio 
- Use case: <mark style="background: #BBFABBA6;">youtube subtitles</mark> 

---
### Amazon Polly 

- turn texts to speech 
- allows to create applications that can talk 

- for pronunciation of stylized words or acronyms use <mark style="background: #BBFABBA6;">Lexicon</mark>
- for customization use <mark style="background: #BBFABBA6;">SSML</mark> (Systhesis markup language)
	- include breathing sound, whispering
	- using newscaster speaking style
	- emphasis on particular words 

--- 

### Amazon Translate 

- Natural and accurate language translation 
- used to localize content for international users 
- translate large volumes of text efficiently 

--- 
# Amazon Lex 

- used for building conversational interfaces (alexa)
- uses ML and NLP to understand the intent and context

difference between lex and transcibe 

| Feature             | **Amazon Lex**                                                            | **Amazon Transcribe**                                       |
| ------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------- |
| **Primary Purpose** | Build chatbots and voice/text-based conversational interfaces             | Transcribe spoken audio into text (speech-to-text)          |
| **Core Technology** | Automatic Speech Recognition (ASR) + Natural Language Understanding (NLU) | Automatic Speech Recognition (ASR) only                     |
| **Output**          | Structured intents and slots for actions (based on user input)            | Text transcription of audio                                 |
| **Capabilities**    | Multi-turn conversations, intent recognition, context handling            | Speaker identification, timestamps, real-time transcription |
| **Use Cases**       | Chatbots, virtual assistants, IVR systems                                 | Transcribing calls, meetings, media files                   |

---

### Amazon Comprehend 

- For NLP, NLP in exam --> Comprehend
- Uses ML to find relationships in text
	- language 
	- emotions
	- key phrases, people, brands
	- analyze text using tokenization and PoS
	- organize text files by topic 

**Medical Comprehend**
- structuring health data from doctors prescriptions or unstructured texts

---

### Amazon SageMaker

- used by developers and data scientists to build ML models 

![[Pasted image 20240924001358.png|500]]

---
### Amazon Forecast

- fully managed 
- uses ML to deliver accurate forecasts
- reduce forecast time from months to hours
- Financial Planning, Resource Planning, Product demand planning 

![[Pasted image 20240924000504.png|500]]

---

### Amazon Kendra 

- document search service - fully managed
- extracts answers from a document 
- learns from user interactions and feedback provided (reinforcement?)

---

### Amazon Personalize

- managed ML service, real time personalization recommendations 
- same technology used on amazon.com 
- buys milk + eggs ---> recommends butter

---
### Amazon Textract

- extract text, handwriting and data from scanned documents 

![[Pasted image 20240924001101.png|500]]

---

### Important for Exam (Summary)

| Service     | Function                                    |
| ----------- | ------------------------------------------- |
| Rekognition | Face detection, labeling, celeb recognition |
| Transcribe  | Audio to text (e.g., Subtitles)             |
| Polly       | Text to audio                               |
| Translate   | Translate large data                        |
| Lex         | Build conversational bots                   |
| Comprehend  | NLP                                         |
| SageMaker   | For developers and data scientists          |
| Forecast    | Forecasts                                   |
| Kendra      | ML-based document search                    |
| Personalize | Real-time personalization                   |

---
Date: 23/09/2024
Vivek Malapaka
____
