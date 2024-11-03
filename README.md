# googlesheetAPI_dataentry
# README: AI-Powered Data Entry Tool for Google Sheets

## Project Overview
This project automates data entry using a Python-based AI agent powered by Ollama and integrated with the Google Sheets API. The AI agent parses user inputs and populates the Google Sheet accurately, reducing manual effort.

## Use Cases
### 1. **Contact List Manager**
- **Purpose**: Build and maintain a contact database by automatically entering names, phone numbers, emails, and other relevant details into a Google Sheet.
- **How**: Modify the input and structure to include additional fields as required.
- **Benefit**: Streamlines the process of maintaining contact lists, useful for networking and job-seeking.

### 2. **Job Application Tracker**
- **Purpose**: Keep track of job applications by logging details such as company name, job title, application date, and status.
- **How**: Customize the data entry structure to include columns for job-related information and statuses (e.g., "applied," "interviewed," "offer received").
- **Benefit**: Helps job seekers stay organized and monitor progress across multiple applications.

## Initial Setup
### Step 1: Download and Install Ollama
- Visit [Ollama.com](https://ollama.com) and download the software. Ensure it is properly installed.

### Step 2: Python Environment
- Create and activate a Python virtual environment:
  ```bash
  python -m venv your_env_name
  source your_env_name/bin/activate  # macOS/Linux
  your_env_name\Scripts\activate   # Windows
  ```

### Step 3: Install Dependencies
- Run the following to install required Python packages:
  ```bash
  pip install google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client Function Calling
  ```

## Google Cloud Configuration
### Step 1: Create a Google Cloud Project
- Go to [Google Cloud Console](https://console.cloud.google.com/) and create a new project.

### Step 2: Set Up OAuth Consent Screen
- Under **APIs & Services**, select **OAuth consent screen**, choose **External**, and provide required details.

### Step 3: Create OAuth Client ID
- Navigate to **Credentials** > **Create Credentials** > **OAuth Client ID**.
- Choose **Desktop App** and download the JSON file as `ClientSecret.json`.

### Step 4: Enable Google Sheets API
- Go to **Library** in **APIs & Services**, search for **Google Sheets API**, and enable it.

## Code Implementation
### `googleapi.py`
Handles authentication and creation of service instances for Google APIs.
```python
import os
import pickle
import google_auth_oauthlib.flow
import googleapiclient.discovery
import googleapiclient.errors

def createService(client_secret_file, api_name, api_version, *scopes):
    token_dir = 'token_files'
    if not os.path.exists(token_dir):
        os.makedirs(token_dir)
    pickle_file = f'{token_dir}/token_{api_name}_{api_version}.pickle'

    credentials = None
    if os.path.exists(pickle_file):
        with open(pickle_file, 'rb') as token:
            credentials = pickle.load(token)
    
    if not credentials or not credentials.valid:
        flow = google_auth_oauthlib.flow.InstalledAppFlow.from_client_secrets_file(
            client_secret_file, scopes
        )
        credentials = flow.run_console()
        with open(pickle_file, 'wb') as token:
            pickle.dump(credentials, token)

    service = googleapiclient.discovery.build(api_name, api_version, credentials=credentials)
    return service
```

### `app.py`
Main script to run the AI-powered data entry tool.
```python
import json
from googleapi import createService
from function_calling import llamaClient

def constructSheetsService():
    CLIENT_SECRET_FILE = 'ClientSecret.json'
    API_NAME = 'sheets'
    API_VERSION = 'v4'
    SCOPES = ['https://www.googleapis.com/auth/spreadsheets']
    return createService(CLIENT_SECRET_FILE, API_NAME, API_VERSION, *SCOPES)

def addSheetEntry(service, spreadsheet_id, first_name, last_name, age):
    range_name = 'Sheet1!A1:C'
    body = {
        'values': [[first_name, last_name, age]]
    }
    result = service.spreadsheets().values().append(
        spreadsheetId=spreadsheet_id,
        range=range_name,
        valueInputOption='RAW',
        insertDataOption='INSERT_ROWS',
        body=body
    ).execute()
    return result

def run():
    model_id = 'lama3.18b'
    client = llamaClient()
    client.pull_model(model_id)
    spreadsheet_id = 'your_google_sheet_id'
    service = constructSheetsService()

    messages = [{'role': 'system', 'content': 'Data entry agent for Google Sheets.'}]
    while True:
        user_input = input("Enter data (or type 'exit' to quit): ")
        if user_input.lower() == 'exit':
            print("Goodbye!")
            break

        messages.append({'role': 'user', 'content': user_input})
        response = client.chat(model_id, messages)

        if 'tool_calls' in response:
            for tool_call in response['tool_calls']:
                function_name = tool_call['name']
                arguments = tool_call['arguments']
                if function_name == 'addSheetEntry':
                    result = addSheetEntry(service, spreadsheet_id, **arguments)
                    print("Entry added successfully.")
        else:
            print("No valid tool call detected.")

if __name__ == "__main__":
    run()
```

## Running the Program
- Run the script:
  ```bash
  python app.py
  ```
- Enter contact or job application data to test the AI agent.
- Type `exit` to stop the program.

## Conclusion
This project demonstrates how to use Python, Ollama, and the Google Sheets API to build a powerful data entry tool. It can be customized for various use cases, such as managing contact lists or tracking job applications.

