### ForesightFin Member Reports API Documentation

Welcome to the **ForesightFin Member Reports API** documentation. This API provides endpoints for retrieving member-related financial data, including active loans, investments, loan repayment summaries, member profiles, and overall account summaries. Below you will find comprehensive information to help you integrate and utilize these endpoints effectively.

## Table of Contents

1. [Base URL](#base-url)
2. [Authentication](#authentication)
3. [Endpoints](#endpoints)
    - [1. Get Active Loans](#1-get-active-loans)
    - [2. Get Investments](#2-get-investments)
    - [3. Get Loan Repayment Summary](#3-get-loan-repayment-summary)
    - [4. Get Member Profile](#4-get-member-profile)
    - [5. Get Account Summary](#5-get-account-summary)
4. [Error Handling](#error-handling)
5. [Testing](#testing)
6. [Examples](#examples)
7. [Contact & Support](#contact--support)

---

## Base URL

All API endpoints are accessible under the following base URL:

https://api.foresightfin.app/

---

## Authentication

*Note: The provided code snippets do not include authentication mechanisms. It is recommended to implement secure authentication (e.g., OAuth 2.0, API keys) to protect your endpoints.*

---

## Endpoints

### 1. Get Active Loans

Retrieve a list of active loan IDs for a specific member and station.

- **URL:** `/active-loans`
- **Method:** `GET`
- **URL Params:**
    - `memberNumber` (string, required): The unique identifier for the member.
    - `stationId` (string, required): The identifier for the station.
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      [
          12345,
          67890,
          23456
      ]
      ```
- **Error Responses:**
    - **Code:** `500 Internal Server Error`
    - **Content:** No content.

---

### 2. Get Investments

Retrieve a list of investments for a specific member, station, and investment code.

- **URL:** `/investments`
- **Method:** `GET`
- **URL Params:**
    - `memberNumber` (string, required): The unique identifier for the member.
    - `stationId` (string, required): The identifier for the station.
    - `investmentCode` (integer, required): The code representing the type of investment. Must be one of the following:

      | Enum Value           | Code |
      |----------------------|------|
      | DEPOSITS             | 96   |
      | SIGHT_DEPOSITS       | 92   |
      | SAVINGS              | 98   |
      | SHARES               | 97   |
      | ADDITIONAL_SHARES    | 95   |

- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      [
          {
              "receiptDate": "2023-01-15",
              "debit": 1000.0,
              "credit": 500.0,
              "runningBalance": 500.0
          },
          {
              "receiptDate": "2023-02-15",
              "debit": 1000.0,
              "credit": 600.0,
              "runningBalance": 900.0
          }
      ]
      ```

---

### 3. Get Loan Repayment Summary

Retrieve detailed information about a specific loan repayment summary for a member at a station.

- **URL:** `/loan-repayment-summary`
- **Method:** `GET`
- **URL Params:**
    - `memberNumber` (string, required): The unique identifier for the member.
    - `stationId` (string, required): The identifier for the station.
    - `loanId` (integer, required): The unique identifier for the loan.
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      [
          {
              "loanId": 101,
              "loanDescription": "Personal Loan",
              "receiptDate": "2023-01-15",
              "transIndicator": "P",
              "disbursedAmount": 5000.0,
              "requestedAmount": 4500.0,
              "paidAmount": 500.0,
              "principalPaid": 300.0,
              "interestPaid": 200.0,
              "principalAmount": 4500.0,
              "cumulativePrincipalPaid": 300.0,
              "cumulativeInterestPaid": 200.0,
              "outstandingPrincipal": 4200.0,
              "outstandingInterest": 1800.0,
              "interestAmount": 500.0
          }
      ]
      ```

---

### 4. Get Member Profile

Retrieve the profile information of a member based on their phone number.

- **URL:** `/member-profile`
- **Method:** `GET`
- **URL Params:**
    - `phoneNumber` (string, required): The phone number of the member in E.164 format (e.g., `+255657822049`).
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      {
          "surname": "Doe",
          "otherName": "John",
          "memberNo": "MEM123",
          "stationId": "STN456",
          "saccoName": "Foresight SACCO"
      }
      ```

---

### 5. Get Account Summary

Retrieve an account summary for a member that includes balances for savings, shares, deposits, and outstanding loans.

- **URL:** `/account-summary`
- **Method:** `GET`
- **URL Params:**
    - `memberNumber` (string, required): The unique identifier for the member.
    - `stationId` (string, required): The identifier for the station.
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      {
          "savingsBalance": 15000.0,
          "sharesBalance": 1000.0,
          "depositsBalance": 5000.0,
          "outstandingLoans": [
              {
                  "loanId": 101,
                  "loanDescription": "Emergency Loan",
                  "outstandingAmount": 4200.0
              },
              {
                  "loanId": 102,
                  "loanDescription": "Personal Loan",
                  "outstandingAmount": 1800.0
              }
          ]
      }
      ```
- **Error Responses:**
    - **Code:** `404 Not Found`
    - **Content:** No content.
    - **Code:** `500 Internal Server Error`
    - **Content:** No content.

- **Example Request:**
    ```
    GET https://api.foresightfin.app/account-summary?memberNumber=MEM123&stationId=STN456
    ```

---

## Error Handling

The API uses standard HTTP status codes to indicate the success or failure of an API request:

- **200 OK:** The request was successful, and the server returned the requested data.
- **400 Bad Request:** The request was invalid or cannot be otherwise served. This is often due to missing required parameters or invalid parameter formats.
- **404 Not Found:** The requested resource could not be found.
- **500 Internal Server Error:** An unexpected error occurred on the server.

*Note: The API currently does not provide detailed error messages in the response body. It is recommended to enhance error responses with meaningful messages for better debugging and user experience.*

---

## Testing

For testing purposes, you can use the following phone numbers to retrieve member profiles:

- **Phone Number 1:** `+255657822049`
- **Phone Number 2:** `+255762415356`

*Ensure that these phone numbers exist in the database to receive successful responses.*

---

## Contact & Support

For any questions or support related to the ForesightFin Member Reports API, please contact developer.

Thank you for using the ForesightFin Member Reports API!
