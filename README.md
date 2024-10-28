<div class="status-bar" style="text-align: center;"> 🛠 Projeto em construção 🛠... </div>

# User Registration with Document Verification

This project is a backend API built with NestJS that enables user registration with automated document verification using AWS services (Textract, S3, DynamoDB, and Lambda), along with email verification using AWS SES.

# 📑 Table of Contents

01. [Overview](#overview)
02. [Technologies Used](#technologies-used)
03. [Setup and Installation](#setup-and-installation)
04. [Project Structure](#project-structure)
05. [API Endpoints](#api-endpoints)
06. [Email Verification Process](#email-verification-process)
07. [Contributing](#contributing)
08. [License](#license)
09. [Courses](#courses)
10. [Author](#author)

<h1 id="overview">📘 Overview </h1>

This system enables user registration with automatic data verification through OCR (Optical Character Recognition) on identity documents (e.g., ID cards, driver's licenses). It leverages AWS services for file storage, OCR, data validation, and database management.

<h1 id="technologies-used">🛠 Technologies Used </h1>

- **NestJS** for backend framework
- **AWS S3** for document storage
- **Amazon Textract** for OCR
- **AWS SES** for email verification
- **AWS Lambda** for serverless validations
- **DynamoDB** for user records database

---
<h1 id="setup-and-installation">⚙️ Setup and Installation </h1>

## Prerequisites

- Node.js and npm/yarn installed
- AWS account with access to S3, Textract, DynamoDB, and Lambda

## Steps

1. **Clone the repository:**
    ```bash
    git clone https://github.com/igorttosta/Document-Validation.git
    ```
2. **Install dependencies:**
    ```bash
    npm install
    ```
3. **Environment variable configuration in the ".env" file:**
    ```plaintext
    AWS_ACCESS_KEY_ID=<your_aws_access_key>
    AWS_SECRET_ACCESS_KEY=<your_aws_secret_key>
    AWS_REGION=<aws_region>
    S3_BUCKET_NAME=<s3_bucket_name>
    DYNAMODB_TABLE_NAME=<dynamodb_table_name>
    SES_EMAIL_SOURCE=<source_email@yourdomain.com>
    ```
4. **Start the development server:**
    ```bash
    npm run start:dev
    ```

<h1 id="project-structure">📂 Project Structure </h1>

```bash
    ├── src
    │   ├── auth                      # Authentication Module
    │   │   ├── auth.controller.ts     # Handles auth-related routes (e.g., email verification)
    │   │   ├── auth.service.ts        # Business logic for authentication and email token handling
    │   │   ├── dtos                   # DTOs for auth requests
    │   │   │   └── verify-email.dto.ts # DTO for email verification request
    │   │   ├── auth.module.ts         # Module setup for auth features
    │   │
    │   ├── users                     # Users Module
    │   │   ├── users.controller.ts    # Handles user-related routes (e.g., registration, upload)
    │   │   ├── users.service.ts       # Business logic for user management
    │   │   ├── dtos                   # DTOs for user requests
    │   │   │   ├── create-user.dto.ts # DTO for user registration
    │   │   │   └── upload-doc.dto.ts  # DTO for document upload
    │   │   ├── users.module.ts        # Module setup for user features
    │   │
    │   ├── aws                       # AWS Integrations Module
    │   │   ├── aws.service.ts         # AWS interactions (S3, Textract, SES)
    │   │   ├── aws.module.ts          # Module setup for AWS integrations
    │   │
    │   ├── main.ts                   # Entry point for the NestJS application
    │   ├── app.module.ts             # Root module of the application
    │
    ├── .env                          # Environment configuration
    └── README.md                     # Documentation for the project
 ```

- auth/dtos: Data Transfer Objects (DTOs) for authentication, including verify-email.dto.ts for email verification.
- users/dtos: DTOs for user module, including create-user.dto.ts for registration and upload-doc.dto.ts for document upload.
- aws: Manages interactions with AWS services such as S3 for storage, Textract for document analysis, and SES for email services.

<h1 id="api-endpoints">🚀 API Endpoints </h1>

## User Registration

- **Route:** `POST /users/register`
- **Description:** Registers a new user
- **Request Body:**
    ```json
    {
        "name": "User's name",
        "email": "email@example.com",
        "cpf": "12345678900",
        "birthDate": "1990-01-01"
    }
    ```

## Document Upload

- **Route:** `POST /users/upload-document`
- **Description:** Uploads an identification document
- **Request Body:** Multipart form with a `file` field

## Document Validation

- **Route:** `POST /users/validate-document`
- **Description:** Validates the document using OCR
- **Request Body:**
    ```json
    {
        "userId": "user_id",
        "documentId": "document_id"
    }
    ```

<h1 id="email-verification-process">📧 Email Verification Process </h1>

## Overview
After registration, the user will receive an email with a verification link. Clicking the link confirms the email associated with the account.

## Steps

1. Generate Verification Token: Upon registration, a unique token is created and stored.
2. Send Verification Email: An email containing the verification link with the token is sent via AWS SES.
3. Verify Token: When the user clicks the link, a verification endpoint validates the token.
4. Update User Status: If valid, the user's email is marked as verified.

## Endpoint

- **Route:** `GET /auth/verify-email`
- **Description:** Verifies the email address using a token
- **Query Parameters:** 
    - **token (string):** The unique token sent to the user's email.

<h1 id="contributing">🤝 Contributing </h1>

Contributions are welcome! To contribute:

- **Fork the project**
- **Create a new branch:** `git checkout -b my-new-feature`
- **Commit your changes:** `git commit -m 'Added a new feature'`
- **Push to the branch:** `git push origin my-new-feature`
- **Open a Pull Request**

<h1 id="license">📜 License </h1>

Distributed under the MIT License. See `LICENSE` for more information.

<h1 id="courses">🎁 Courses that helped me </h1>

- [NestJS](https://www.udemy.com/course/nestjs-do-zero)
- [AWS Serverless](https://www.udemy.com/course/aws-serverless-nodejs-cdk-pt)

<h1 id="author">✒️ Author </h1>

Made by **Igor T Matos**. For more information: my [LinkedIn](https://www.linkedin.com/in/matos-igor-tosta/)
