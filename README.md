# Megloo Re:Turn System (Lending Client)
## Overview

This repository contains the client-side implementation for the Megloo Re:Turn System, a reusable food container lending platform deployed at Keio University SFC (Wada Lab).

The application operates as a LINE LIFF (LINE Front-end Framework) web app. It scans QR codes attached to containers, authenticates the user via LINE, and transmits transaction data to a serverless backend.

## System Architecture

The system follows a decoupled client-server architecture:

- Frontend (Client): Static HTML/CSS/JS hosted on GitHub Pages.

- Backend (API): Google Apps Script (GAS) deployed as a Web App.

- Database: Google Sheets (managed by GAS).

- Authentication: LINE Login (OpenID Connect) via LIFF SDK.

## Data Flow

User scans QR Code -> Opens LIFF URL with Container ID parameter.

Client parses URL parameters (?id=00001).

Client authenticates user and retrieves sub (User ID) via liff.getDecodedIDToken().

Client sends POST request to GAS API Endpoint.

GAS appends transaction log to Google Sheets and triggers a LINE Push Message.

## Technology Stack
Frontend: HTML5, CSS3, Vanilla JavaScript (ES6+)

SDK: LINE LIFF SDK v2

Backend: Google Apps Script (GAS)

Infrastructure: GitHub Pages (Hosting)

## Configuration
To deploy this client, the following constants must be configured in index.html:

### JavaScript

// The endpoint URL of the deployed Google Apps Script Web App
const GAS_API_URL = "https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec";

// The LIFF ID obtained from LINE Developers Console
const MY_LIFF_ID = "YOUR_LIFF_ID"; 

- API Specification

    The frontend communicates with the backend via an HTTP POST request. Due to CORS restrictions on Google Apps Script, the request is sent using mode: 'no-cors'.

- Endpoint URL: Defined in GAS_API_URL

- Method: POST

- Content-Type: application/json

- Request Payload
```JSON

{
  "userId": "U1234567890abcdef...", 
  "containerId": "00001"
}
```

## Setup and Deployment
- Backend Deployment:

    Deploy the Google Apps Script project as a Web App.

    Set access permissions to "Anyone".

- Frontend Deployment:

    Upload index.html and assets to this repository.

    Enable GitHub Pages for the main branch.

- LINE Developers Console Configuration:

    Set the Endpoint URL of the LIFF app to the GitHub Pages URL.

    Ensure Scopes include openid and profile.

## License and Credits
System Designed & Developed by Kouzen Jo 
Affiliation: Wada Lab, Keio Univ. SFC
PM: Megloo Inc.
Collaborating Org: Kobayashi Create Inc.

Copyright (c) 2025. Kouzen Jo. All rights reserved.