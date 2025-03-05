# API Documentation

## **Survey API**

[View ERD Diagram](https://drive.google.com/file/d/1eLUdc5WBJ5WGq-nJCDCSfphmNCSCDlVY/view?usp=sharing)

## **1. GET All Surveys**
**Endpoint:**
```
GET /api/surveys
```
**Response:**

| Field           | Type    | Description                 |
|-----------------|---------|-----------------------------|
| msg             | string  | Response message            |
| code            | string  | Response code               |
| data            | object  | Survey data                 |
| data.id         | string  | Survey ID                   |
| data.title      | string  | Survey title                |
| data.desc       | string  | Survey description          |
| data.status     | number  | Survey status (0 or 1)      |
| data.questions  | array | List of survey questions |

#### **Question Object**
| Field       | Type   | Description                            |
|-------------|--------|----------------------------------------|
| id          | string | Question ID                            |
| type        | string | Question type (`short_text`, `long_text`, `multiple_choice`, `dropdown`, `yes_no`, `file_upload`)|
| label       | string | Question text                          |
| desc        | string | Question additional description        |
| settings    | object | Configuration based on question `type` |

### **Settings Per Type**
Berikut adalah kemungkinan `settings` berdasarkan `type`:

#### **1. Short Text , Long Text (`type: "short_text and long_text"`)**
```json
{
  "required": true,
  "max_character": 100
}
```

#### **2. Multiple Choice (`type: "multiple_choice"`)**
```json
{
  "required": true,
  "multiple_selection": false,
  "min_selection":1,
  "max_selection":1,
  "other_option": false
}
```

#### **3. Dropdown, Yes No, File Upload (`type: "dropdown, yes_no and file_upload"`)**
```json
{
  "required": true,
}
```


**Response Example:**
```json
{
  "msg": "success",
  "code": "0",
  "data": {
      "pages": 9,
      "total": 85,
      "records":[
        {
        "id": "survey-123",
        "title": "Customer Satisfaction Survey",
        "desc": "Help us improve our service",
        "status": 1,
        "questions":  [
              {
                  "id": "1",
                  "type": "short_text",
                  "label": "What is your name?",
                  "desc": "",
                  "settings": {
                      "required": true,
                      "max_character": 100
                  }
              },
              {
                  "id": "2",
                  "type": "long_text",
                  "label": "Describe your role and responsibilities",
                  "desc": "",
                  "settings": {
                      "required": true,
                      "max_character": 500
                  }
              },
              {
                  "id": "3",
                  "type": "multiple_choice",
                  "label": "Which programming languages do you use regularly",
                  "desc": "",
                  "options": [
                      { "id": "1", "label": "JavaScript" },
                      { "id": "2", "label": "Python" },
                      { "id": "3", "label": "Java" },
                      { "id": "4", "label": "PHP" }
                  ],
                  "settings": {
                      "required": true,
                      "multiple_selection": true,
                      "min_selection": 1,
                      "max_selection": 4,
                      "other_option": false
                  }
              },
              {
                  "id": "4",
                  "type": "dropdown",
                  "label": "What is your primary development focus?",
                  "desc": "",
                  "options": [
                      { "id": "1", "label": "Frontend" },
                      { "id": "2", "label": "Backend" },
                      { "id": "3", "label": "Full Stack" },
                      { "id": "4", "label": "DevOps" }
                  ],
                  "settings": {
                      "required": true
                  }
              },
              {
                  "id": "5",
                  "type": "yes_no",
                  "label": "Are you interested in mentoring junior,developers?",
                  "desc": "",
                  "settings": {
                      "required": true
                  }
              },
              {
                  "id": "6",
                  "type": "file_upload",
                  "label": "Upload a sample of your recent work",
                  "desc": "",
                  "settings": {
                      "required": true
                  }
              }
          ]
        }
      ]
  }
}
```

---

## **2. GET Single Survey by ID**
**Endpoint:**
```
GET /api/surveys/{id}
```
**Response:**

| Field           | Type    | Description                    |
|-----------------|---------|--------------------------------|
| msg             | string  | Response message               |
| code            | string  | Response code                  |
| data            | object  | Survey data                    |
| data.id         | string  | Survey ID                      |
| data.title      | string  | Survey title                   |
| data.desc       | string  | Survey description             |
| data.status     | number  | Survey status (0 or 1)         |
| data.questions  | array   | List of survey questions       |


**Response Example:**
```json
{
  "msg": "success",
  "code": "200",
  "data": {
    "id": "1",
    "title": "Customer Satisfaction Survey",
    "desc": "Help us improve our service",
    "status": 1,
    "questions": [
      {
        "id": "1",
        "type": "short_text",
        "label": "What is your name?",
        "desc": "",
        "settings": {
          "required": true,
          "max_character": 100
        }
      },
      {
        "id": "2",
        "type": "multiple_choice",
        "label": "How satisfied are you with our service?",
        "desc": "",
        "options": [
          { "id": "1", "label": "Very Satisfied" },
          { "id": "2", "label": "Satisfied" },
          { "id": "3", "label": "Neutral" },
          { "id": "4", "label": "Dissatisfied" }
        ],
        "settings": {
          "required": true,
          "multiple_selection": false,
          "min_selection": 1,
          "max_selection": 1
        }
      }
    ]
  }
}
```

---

## **3.POST Create Survey**
**Endpoint:**
```
POST /api/surveys
```
**Payload:**
| Field       | Type    | Description                    |
|-------------|---------|--------------------------------|
| title       | string  | survey title                   |
| desc        | string  | survey description             |


**Request Payload Example:** 
```json
{
  "title": "New Survey",
  "desc": "Survey Description",
}
```

**Request Response Example:** 
```json
{
  "code":"0",
  "msg":"success",
  "data":{
    "id": "1",
    "title": "Customer Satisfaction Survey",
    "desc": "Help us improve our service",
    "status": 0,
    "questions": []
  }
}
```
 
---

## **4. PUT Update Survey**
**Endpoint:**
```
PUT /api/surveys
```
**Request Payload:**

| Field           | Type   | Description                |
|-----------------|--------|----------------------------|
| surveyId        | string | Survey id                  |
| title           | string | Survey title               |
| desc            | string | Survey description         |
| status          | number | Survey status (0 or 1)     |
| addedQuestions  | array  | List of new questions      |
| updatedQuestions| array  | List of updated questions  |


**Request Payload Example:**
```json
{
  "surveyId": "1"
  "title": "New Survey",
  "desc": "Survey Description",
  "status": 1,
  "addedQuestions": [
    {
        "type": "multiple_choice",
        "label": "How satisfied are you with our service?",
        "desc": "",
        "options": [
          { "id": "1", "label": "Very Satisfied" },
          { "id": "2", "label": "Satisfied" },
          { "id": "3", "label": "Neutral" },
          { "id": "4", "label": "Dissatisfied" }
        ],
        "settings": {
          "required": true,
          "multiple_selection": false,
          "min_selection": 1,
          "max_selection": 1
        }
    },
    {
        "type": "yes_no",
        "label": "Are you satisfied with our service?",
        "desc": "",
        "options": [],
        "settings": {
          "required": true,
        }
    },
  ],
  "updatedQuestions": [
    {
      "id": "1",
      "text": "What is your age?",
      "type": "short_text",
      "settings": {
        "required": true,
        "max_character": '1000'
      }
    }
  ]
}
```

**Response Example:**
```json
{
  "code": "0",
  "msg":"success",
  "data": {
  "title": "New Survey",
  "desc": "Survey Description",
  "status": 1,
  "questions": [
      {
        "id": 1,
        "text": "What is your age?",
        "type": "short_text",
        "settings": {
          "required": true
        }
      },
      {
          "id": 2,
          "type": "multiple_choice",
          "label": "How satisfied are you with our service?",
          "desc": "",
          "options": [
            { "id": "1", "label": "Very Satisfied" },
            { "id": "2", "label": "Satisfied" },
            { "id": "3", "label": "Neutral" },
            { "id": "4", "label": "Dissatisfied" }
          ],
          "settings": {
            "required": true,
            "multiple_selection": false,
            "min_selection": 1,
            "max_selection": 1
          }
      },
      {
          "id": 2,
          "type": "yes_no",
          "label": "Are you satisfied with our service?",
          "desc": "",
          "options": [],
          "settings": {
            "required": true,
          }
      },
    ]
  }
}
```

---

## **5. DELETE Question**
**Endpoint:**
```
DELETE /api/surveys/{survey_id}/questions/{question_id}
```
**Response:**

| Field   | Type   | Description        |
|---------|--------|--------------------|
| msg     | string | Response message   |
| code    | string | Response code      |

**Response Example:**
```json
{
  "code": "0",
  "msg": "Question deleted successfully",
}
```

---

### **6. GET All Responses By Survey ID**
**Endpoint:**
```
GET /api/surveys/{id}/responses
```
**Response:**

| Field    | Type        | Description           |
|----------|------- -----|-----------------------|
| msg      | string      | Response message      |
| code     | string      | Response code         |
| data     | Responses[] | List of responses     |


**Data Responses Object**
| Field                 | Type   | Description    |
|-----------------------|--------|----------------|
| id                    | string | response id    |
| surveyId              | string | survey id      |
| user                  | string | question id    |
| created_at            | string | created time   |
| answers               | array  | asnwers list   |
| answers[].questionId  | string | question id    |
| answers[].response    | string | answer         |


**Response Example:**
```json
{
  "msg": "Success get responses",
  "code": "200",
  "data": [
    {
      "id": "resp-123",
      "user": "user-456",
      "created_at":"2023-12-01T12:00:00Z",
      "answers": [
        {
          "questionId": "q-1",
          "response": "Very Satisfied"
        }
      ],
    }
  ]
}
```

---

## **7. POST Submit Survey**
**Endpoint:**
```
POST /api/surveys/{id}/submit
```
**Request Payload:**


**Request Example:**
```json
{}
```

**Response:**

| Field   | Type   | Description         |
|---------|--------|---------------------|
| msg     | string | Response message    |
| code    | string | Response code       |

**Response Example:**
```json
{
  "code": "0",
  "msg": "Survey submitted successfully"
}
```

<!-- --- 

### **Optional: GET Show Survey Answer (H5)**
**Endpoint:**
```
GET /api/surveys/{id}/answers
```
**Response:** *(Same as GET All Responses)* -->

## **Interface Definitions**

### **Survey Interface**
```typescript
interface Survey {
  id: string;
  title: string;
  desc: string;
  status: 0 | 1;
  questions: Question[];
}
```

### **Question Interface**
```typescript
interface Question {
  id: string;
  surveyId: string;
  text: string;
  type: 'short_text' | 'long_text' | 'multiple_choice' | 'yes_no' | 'dropdown' | 'file_upload';
  options?: QuestionOption[];
  settings?:[]
}
```

### **QuestionOption Interface**
```typescript
interface QuestionOption {
  id: string;
  label: string;
}
```

### **SurveyResponse Interface**
```typescript
interface SurveyResponse {
  id: string;
  surveyId: string;
  user: string;
  answers: Answer[];
  created_at: string;
}
```

### **Answer Interface**
```typescript
interface Answer {
  questionId: string;
  response: string | string[];
}
```
