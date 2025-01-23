# Server Message Board

This project is a simple serverless message board hosted on AWS S3 and integrated with an AWS API Gateway endpoint (backed by Lambda or other AWS services). Users can post messages via the web UI, and the messages are fetched and displayed in real time.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Deploying](#deploying)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [License](#license)

## Overview

- [Visit the Message Board](http://messageboard-bucket-490r.s3-website-us-east-1.amazonaws.com)

This message board allows users to post short messages, which are then displayed on the page. The front-end is a static website hosted on Amazon S3. When a user submits a message, the front-end calls an AWS API Gateway endpoint that handles creation and retrieval of messages.

## Features

- **Post new messages**: Users can submit messages using the text area and Submit button.
- **View existing messages**: Users can view all previously submitted messages.
- **Refresh messages**: Users can refresh the message list at any time to retrieve the latest entries.
- **Hosted on AWS S3**: The application is served as a static website from an S3 bucket.
- **Serverless architecture**: The back-end is powered by AWS API Gateway and AWS Lambda (or another AWS service behind API Gateway), which means there is no need to manage servers.

## Architecture

1. **Front-end**:
   - A static HTML/CSS/JavaScript website.
   - Hosted on an Amazon S3 bucket configured for static website hosting.
2. **API**:
   - AWS API Gateway endpoint (e.g., `https://adyy6bp186.execute-api.us-east-1.amazonaws.com/prod/messages`) to handle `POST` and `GET` requests.
   - AWS Lambda (or another service) is triggered by API Gateway to handle the database operations (read/write messages).

The communication flow is:
```
Browser (HTML/JS) -> S3 (Static Files)
                 -> API Gateway -> Lambda -> Data Store
```

## Getting Started

### Prerequisites

- **AWS Account**: You need an AWS account to deploy the S3 bucket, API Gateway, and Lambda functions.
- **AWS CLI** (optional, for more automated deployment).
- **Basic Web Development Tools**: A code editor, a browser, and knowledge of HTML, CSS, and JavaScript.

### Deploying

1. **Create an S3 Bucket**:
   - Go to the S3 console in AWS.
   - Create a new bucket (publicly accessible for website hosting).
   - Enable static website hosting under the bucket’s **Properties** tab.

2. **Upload `index.html` (and any other assets)**:
   - Upload the `index.html` file (and any CSS/JS if separate) to the S3 bucket.
   - Make sure the files are set to **public read** or the bucket policy allows public read.

3. **Set up API Gateway**:
   - Create a new API in API Gateway.
   - Define the `POST /messages` method to accept a JSON body (`{ "message": "some text" }`).
   - Define the `GET /messages` method to fetch existing messages.

4. **Link API Gateway to Lambda (or another service)**:
   - Create or configure a Lambda function that handles reading/writing messages (e.g., in DynamoDB).
   - Give the Lambda function permission to access your data store.
   - Configure your API Gateway to integrate with the Lambda function.

5. **Update the Front-end**:
   - In the `index.html` file, update the `apiEndpoint` variable to match your API Gateway endpoint.
   - Example: `const apiEndpoint = 'https://{api-id}.execute-api.us-east-1.amazonaws.com/prod';`

6. **Test**:
   - Open the S3 website URL in your browser.
   - Post a message and refresh to see it displayed.

## Usage

1. **Access the Application**:
   - Go to the [live URL](http://messageboard-bucket-490r.s3-website-us-east-1.amazonaws.com).

2. **Posting a Message**:
   - Type your message in the text area under **"Post a Message"**.
   - Click **Submit**. You should see an alert indicating the message was posted successfully.

3. **Viewing Messages**:
   - Scroll down to the **"Messages"** section or click **Refresh Messages** to load any new messages.

4. **Refreshing**:
   - Click the **Refresh Messages** button to fetch the latest messages from the server.

## Project Structure

```
.
├── index.html    // Main HTML file (frontend code)
└── README.md     // Project documentation
```
