
# API Documentation

## 1. AI Detection Router (`/detect-coin-ai`)

### **Description**
This API accepts an image file and uses OpenAI GPT-4 to identify and return information about the coin.

### **Method**
- **POST**

### **Endpoint**
```
/detect-coin-ai
```

### **Request**

- **File**: The image file must be attached with the key `file`.

#### **Request Body**:
- Multipart Form Data with an image file.

### **Response**:
- **200 OK**: Returns the result of coin identification.
  - **Body**: JSON
    ```json
    {
      "result": "Coin name or error"
    }
    ```

- **400 Bad Request**: When no file is attached or the file is empty.
  - **Body**: JSON
    ```json
    {
      "error": "No file provided" or "Empty file"
    }
    ```

- **500 Internal Server Error**: If an error occurs during processing.
  - **Body**: JSON
    ```json
    {
      "error": "Error description"
    }
    ```

---

## 2. LLM Router (`/ask`)

### **Description**
This API accepts a question in JSON format and returns an answer from the chatbot model.

### **Method**
- **POST**

### **Endpoint**
```
/ask
```

### **Request**

- **Body Request**: JSON containing the question.
    ```json
    {
      "question": "Your question here"
    }
    ```

### **Response**:
- **200 OK**: Returns the chatbot's answer.
  - **Body**: JSON
    ```json
    {
      "answer": "Answer from the chatbot"
    }
    ```

- **400 Bad Request**: If the `question` parameter is missing.
  - **Body**: JSON
    ```json
    {
      "error": "Missing 'question' parameter"
    }
    ```

---

## 3. Recognition Router (`/recognize`)

### **Description**
This API accepts an image file, detects coins, removes the background, uses a CNN model to classify the coin, and returns information from the database.

### **Method**
- **POST**

### **Endpoint**
```
/recognize
```

### **Request**

- **File**: The image file must be attached with the key `image`.

#### **Request Body**:
- Multipart Form Data with the image file.

### **Response**:
- **200 OK**: Returns coin information if detected successfully.
  - **Body**: JSON
    ```json
    {
      "class": "Coin class name",
      "confidence": "Confidence level",
      "coin_info": {
        "TENXU": "Coin name",
        "TENQG": "Country name"
      }
    }
    ```

- **400 Bad Request**: If coin detection fails or cannot be identified.
  - **Body**: JSON
    ```json
    {
      "error": "Error description"
    }
    ```

- **404 Not Found**: If no data is found in the database for the detected coin.
  - **Body**: JSON
    ```json
    {
      "class": "Coin class name",
      "confidence": "Confidence level",
      "error": "No data found in the database"
    }
    ```

- **500 Internal Server Error**: If an error occurs during processing.
  - **Body**: JSON
    ```json
    {
      "error": "Network error"
    }
    ```
