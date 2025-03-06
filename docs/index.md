# Survey API & Database Documentation


[View ERD Diagram](https://drive.google.com/file/d/1eLUdc5WBJ5WGq-nJCDCSfphmNCSCDlVY/view?usp=sharing)

## **Database Table Stucture and Sample Data**

### **Tabel `survey`**
| Nama Field   | Tipe Data | Nullable | Default |description |
|-------------|----------|----------|---------|--------------|
| id          | INT      | NO       | AUTO_INCREMENT |
| title       | VARCHAR(255) | NO    | NULL    |
| description | TEXT     | YES      | NULL    |
| created_at  | DATETIME | NO       | CURRENT_TIMESTAMP |
| updated_at  | DATETIME | NO       | CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

**Sample Data:**
| id | title | description | created_at | updated_at |
|----|-------|-------------|------------|------------|
| 1 | Survei Pengalaman Pengguna | Survei untuk mengumpulkan feedback pengguna | 2024-03-06 10:00:00 | 2024-03-06 10:00:00 |

### **Tabel `question`**
| Nama Field         | Tipe Data | Nullable | Default |description |
|-------------------|------------|----------|---------|--------------|
| id               | INT          | NO       | AUTO_INCREMENT |
| survey_id        | INT          | NO       | NULL    |
| type            | VARCHAR(50)   | NO       | NULL    |
| label           | TEXT         | NO       | NULL    |
| description     | TEXT    |  YES       | NULL    |
| required        | BOOLEAN      | NO       | true       |
| multiple_selection | BOOLEAN   | YES      | NULL    |
| min_selection   | INT          | YES      | NULL    |
| max_selection   | INT          | YES      | NULL    |
| other_option    | BOOLEAN      | YES      | NULL    |
| created_at      | DATETIME     | NO       | CURRENT_TIMESTAMP |
| updated_at      | DATETIME     | NO       | CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

**Sample Data:**
| id | survey_id | type | label | required | multiple_selection | min_selection | max_selection | other_option | created_at | updated_at |
|----|-----------|------|-------|----------|-------------------|---------------|---------------|--------------|------------|------------|
| 1 | 1 | short_text | Siapa nama Anda? | true | NULL | NULL | NULL | NULL | 2024-03-06 10:01:00 | 2024-03-06 10:01:00 |
| 2 | 1 | long_text | Ceritakan pengalaman Anda menggunakan produk kami | true | NULL | NULL | NULL | NULL | 2024-03-06 10:02:00 | 2024-03-06 10:02:00 |
| 3 | 1 | multiple_choice | Fitur apa yang paling sering Anda gunakan? | true | true | 1 | 4 | true | 2024-03-06 10:03:00 | 2024-03-06 10:03:00 |
| 4 | 1 | dropdown | Berapa lama Anda telah menggunakan produk kami? | true | NULL | NULL | NULL | NULL | 2024-03-06 10:04:00 | 2024-03-06 10:04:00 |
| 5 | 1 | yes_no | Apakah Anda akan merekomendasikan produk kami? | true | NULL | NULL | NULL | NULL | 2024-03-06 10:05:00 | 2024-03-06 10:05:00 |
| 6 | 1 | file_upload | Unggah screenshot masalah yang Anda temui | true | NULL | NULL | NULL | NULL | 2024-03-06 10:06:00 | 2024-03-06 10:06:00 |

### **Tabel `options`**
| Nama Field  | Tipe Data     | Nullable | Default |description |
|------------|--------------|----------|---------|--------------|
| id         | INT          | NO       | AUTO_INCREMENT |
| question_id | INT         | NO       | NULL    |
| options_text | VARCHAR(255) | NO       | NULL    |
| created_at | DATETIME     | NO       | CURRENT_TIMESTAMP |
| updated_at | DATETIME     | NO       | CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

**Sample Data:**
| id | question_id | options_text | created_at | updated_at |
|----|-------------|--------------|------------|------------|
| 1 | 3 | Dashboard | 2024-03-06 10:07:00 | 2024-03-06 10:07:00 |
| 2 | 3 | Reporting | 2024-03-06 10:07:00 | 2024-03-06 10:07:00 |
| 3 | 3 | Analytics | 2024-03-06 10:07:00 | 2024-03-06 10:07:00 |
| 4 | 3 | Other | 2024-03-06 10:07:00 | 2024-03-06 10:07:00 |
| 5 | 4 | < 1 bulan | 2024-03-06 10:08:00 | 2024-03-06 10:08:00 |
| 6 | 4 | 1-6 bulan | 2024-03-06 10:08:00 | 2024-03-06 10:08:00 |
| 7 | 4 | 6-12 bulan | 2024-03-06 10:08:00 | 2024-03-06 10:08:00 |
| 8 | 4 | > 12 bulan | 2024-03-06 10:08:00 | 2024-03-06 10:08:00 |

### **Tabel `response`**
| Nama Field  | Tipe Data  | Nullable | Default | description |
|------------|-------------|----------|----------|-------------|
| id         | INT         | NO       | AUTO_INCREMENT |             |
| survey_id  | INT         | NO       | NULL     |             |
| user_id    | INT         | YES      | NULL     |             |
| created_at | DATETIME    | NO       | CURRENT_TIMESTAMP |      |

**Sample Data:**
| id | survey_id | user_id | created_at |
|----|-----------|---------|------------|
| 1 | 1 | 101 | 2024-03-06 10:10:00 |

### **Tabel `answer`**
| Nama Field   | Tipe Data  | Nullable | Default | description |
|--------------|------------|----------|----------|-------------|
| id           | INT        | NO       | AUTO_INCREMENT | |
| response_id  | INT        | NO       | NULL    | |
| question_id  | INT        | NO       | NULL    | |
| answer_text  | TEXT       | YES      | NULL    | to store asnwer data except multiple_choice and dropdown |
| option_id    | INT        | YES      | NULL    | |
| other_answer | TEXT       | YES      | NULL    | to store data from multiple_choice other option |
| created_at   | DATETIME   | NO       | CURRENT_TIMESTAMP | |

**Sample Data:**
| id | response_id | question_id | answer_text | option_id | other_answer | created_at |
|----|-------------|-------------|-------------|-----------|--------------|------------|
| 1 | 1 | 1 | John Doe | NULL | NULL | 2024-03-06 10:11:00 |
| 2 | 1 | 2 | Produk sangat membantu pekerjaan saya... | NULL | NULL | 2024-03-06 10:11:00 |
| 3 | 1 | 3 | NULL | 1 | NULL | 2024-03-06 10:11:00 |
| 4 | 1 | 3 | NULL | 2 | NULL | 2024-03-06 10:11:00 |
| 5 | 1 | 3 | NULL | NULL | Fitur Export | 2024-03-06 10:11:00 |
| 6 | 1 | 4 | NULL | 7 | NULL | 2024-03-06 10:11:00 |
| 7 | 1 | 5 | Yes | NULL | NULL | 2024-03-06 10:11:00 |
| 8 | 1 | 6 | screenshot.png | NULL | NULL | 2024-03-06 10:11:00 |
| 9 | 2 | 3 | NULL | 1 | NULL | 2024-03-06 11:00:00 |
| 10 | 2 | 3 | NULL | 3 | NULL | 2024-03-06 11:00:00 |
| 11 | 2 | 3 | NULL | NULL | Custom Analytics | 2024-03-06 11:00:00 |

---

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

**Question Object**
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
| Field       | Type    | Description                   |
|-------------|---------|-------------------------------|
| title       | string  | survey title                  |
| desc        | string  | survey description (optional) |


**Request Payload Example:** 
```json
{
  "title": "New Survey",
  "desc": "Survey Description" (optional),
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

| Field           | Type   | Description                          |
|-----------------|--------|--------------------------------------|
| surveyId        | string | Survey id                            |
| title           | string | Survey title                         |
| desc            | string | Survey description                   |
| status          | number | Survey status (0 or 1)               |
| addedQuestions  | array  | List of new questions (optional)     |
| updatedQuestions| array  | List of updated questions (optional) |


**Request Payload Example:**
```json
{
  "surveyId": "1",
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

## **6. POST Submit Survey**
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


## **Interface Definitions**

### **Survey Interface**
```typescript
interface Survey {
  id: string;
  title: string;
  desc: string;
  status: 0 | 1;
  questions: Question[] | [];
}
```

### **Question Interface**
```typescript
interface Question {
  id: string;
  surveyId: string;
  text: string;
  type: 'short_text' | 'long_text' | 'multiple_choice' | 'yes_no' | 'dropdown' | 'file_upload';
  options?: QuestionOption[] | [];
  settings?:QuestionSettings[] | []
}
```

### **QuestionSettings Interface**
```typescript
 interface QuestionSettings {
  required: boolean;
  max_character?: number;
  multiple_selection?: boolean;
  min_selection?: number;
  max_selection?: number;
  other_option?: boolean;
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





