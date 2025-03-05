# API Documentation

## **Survey API**

### **1. GET All Surveys**
**Endpoint:**
```
GET /api/surveys
```
**Response:**

| Field    | Type     | Description                 |
|----------|---------|-----------------------------|
| msg      | string  | Response message            |
| code     | string  | Response code               |
| data     | object  | Survey data                 |
| data.id  | string  | Survey ID                   |
| data.title | string | Survey title                |
| data.desc | string | Survey description          |
| data.status | number | Survey status (0 or 1)     |
| data.options | array | Additional options         |
| data.questions | array | List of questions         |
| data.questions[].id | string | Question ID        |
| data.questions[].type | string | Question type    |
| data.questions[].label | string | Question label  |

---

### **2. GET Single Survey by ID**
**Endpoint:**
```
GET /api/surveys/{id}
```
**Response:** *(Same as GET All Surveys but only for a single survey)*

---

### **3. POST Create Survey**
**Endpoint:**
```
POST /api/surveys
```
**Request Payload:**

| Field   | Type   | Description            |
|---------|-------|------------------------|
| title   | string | Survey title           |
| desc    | string | Survey description     |
| status  | number | Survey status (0 or 1) |
| options | array  | Additional options     |
| questions | array | List of questions     |

**Response:**

| Field   | Type   | Description         |
|---------|-------|---------------------|
| msg     | string | Response message   |
| code    | string | Response code      |
| data    | object | Created survey data |

---

### **4. PUT Update Survey**
**Endpoint:**
```
PUT /api/surveys/{id}
```
**Request Payload:** *(Same as POST Create Survey)*

**Response:** *(Same as POST Create Survey)*

---

### **5. POST Submit Survey**
**Endpoint:**
```
POST /api/surveys/{id}/submit
```
**Request Payload:**

| Field    | Type   | Description                     |
|----------|-------|---------------------------------|
| answers  | array | List of submitted answers      |
| answers[].question_id | string | Question ID      |
| answers[].response | string | User response     |

**Response:**

| Field   | Type   | Description         |
|---------|-------|---------------------|
| msg     | string | Response message   |
| code    | string | Response code      |

---

### **6. DELETE Question**
**Endpoint:**
```
DELETE /api/surveys/{survey_id}/questions/{question_id}
```
**Response:**

| Field   | Type   | Description         |
|---------|-------|---------------------|
| msg     | string | Response message   |
| code    | string | Response code      |

---

### **7. GET All Responses**
**Endpoint:**
```
GET /api/surveys/{id}/responses
```
**Response:**

| Field    | Type   | Description                      |
|----------|-------|----------------------------------|
| msg      | string | Response message                |
| code     | string | Response code                   |
| data     | array  | List of responses               |
| data[].id | string | Response ID                     |
| data[].user | string | User who submitted the response |
| data[].answers | array | List of answers              |

---

### **Optional: GET Show Survey Answer (H5)**
**Endpoint:**
```
GET /api/surveys/{id}/answers
```
**Response:** *(Same as GET All Responses)*

