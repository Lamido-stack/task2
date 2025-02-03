# Classify-Number API

The **Classify-Number API** is a RESTful service that provides various mathematical properties of a given number. It checks whether the number is prime, perfect, Armstrong, odd/even, calculates the sum of its digits, and returns a fun fact about the number.

## Table of Contents
1. [Overview](#overview)
2. [Endpoint](#endpoint)
3. [Request Parameters](#request-parameters)
4. [Response Formats](#response-formats)
5. [Error Handling](#error-handling)
6. [Example Usage](#example-usage)
7. [Fun Fact Source](#fun-fact-source)
8. [Installation](#installation)

## Overview
The Classify-Number API allows you to send a number and receive back various mathematical properties, including whether the number is:
- Prime
- Perfect
- Armstrong
- Odd/Even

In addition, the API calculates the digit sum of the number and fetches a fun fact about it.

## Endpoint

```
GET /api/classify-number?number=<number>
```

### Parameters
- `number` (required): The number you want to classify. This should be a positive integer.

## Request Parameters

| Parameter  | Type   | Description                              |
|------------|--------|------------------------------------------|
| `number`   | integer| The number to be analyzed. Must be a positive integer. |

### Example Request:
```
GET /api/classify-number?number=371
```

## Response Formats

### 200 OK (Success)
When the request is valid and processed successfully, the API responds with a JSON object containing the following properties:

```json
{
    "number": 371,
    "is_prime": false,
    "is_perfect": false,
    "properties": ["armstrong", "odd"],
    "digit_sum": 11,
    "fun_fact": "371 is an Armstrong number because 3^3 + 7^3 + 1^3 = 371"
}
```

#### Fields in the Response:
- `number` (integer): The number sent in the request.
- `is_prime` (boolean): Whether the number is prime.
- `is_perfect` (boolean): Whether the number is a perfect number.
- `properties` (array of strings): List of properties such as "armstrong", "odd", etc.
- `digit_sum` (integer): The sum of the digits of the number.
- `fun_fact` (string): A fun fact about the number fetched from the Numbers API.

### 400 Bad Request (Error)
If the `number` parameter is missing, invalid, or non-numeric, the API will return a `400` error with an error message:

```json
{
    "number": "alphabet",
    "error": true
}
```

#### Fields in the Error Response:
- `number`: The invalid number or value sent in the request.
- `error`: A boolean value indicating that an error occurred.

## Error Handling
- **Invalid Input**: If the `number` parameter is not a valid integer or is missing, the API will return a `400` status code with an error message.
- **External Errors**: If the Numbers API cannot return a fun fact, the API will return a default message indicating that no fun fact is available.

## Example Usage

### Request:
```bash
GET http://your-url/api/classify-number?number=371
```

### Response:
```json
{
    "number": 371,
    "is_prime": false,
    "is_perfect": false,
    "properties": ["armstrong", "odd"],
    "digit_sum": 11,
    "fun_fact": "371 is an Armstrong number because 3^3 + 7^3 + 1^3 = 371"
}
```

### Example with Invalid Input:
```bash
GET http://your-url/api/classify-number?number=abc
```

Response:
```json
{
    "number": "abc",
    "error": true
}
```

## Fun Fact Source

The fun fact is fetched from [Numbers API](http://numbersapi.com/). This API provides interesting facts about numbers, and the Classify-Number API integrates this source to enrich the response with a fun tidbit about the number.

## Installation

To set up this API locally, follow the steps below.

### Prerequisites
- Python 3.x
- `pip` (Python package manager)

### 1. Clone the repository:
```bash
git clone https://github.com/your-repository/classify-number-api.git
cd classify-number-api
```

### 2. Install required dependencies:
```bash
pip install -r requirements.txt
```

### 3. Run the Flask application:
```bash
python app.py
```

This will start the Flask server, and the API will be available locally at `http://localhost:5000`.