# README: AI-Powered Data Entry Tool for Google Sheets

## Table of Contents
- [Project Overview](#project-overview)
- [Use Cases](#use-cases)
  - [Contact List Manager](#1-contact-list-manager)
  - [Job Application Tracker](#2-job-application-tracker)
- [Initial Setup](#initial-setup)
  - [Step 1: Download and Install Ollama](#step-1-download-and-install-ollama)
  - [Step 2: Python Environment](#step-2-python-environment)
  - [Step 3: Install Dependencies](#step-3-install-dependencies)
- [Google Cloud Configuration](#google-cloud-configuration)
  - [Step 1: Create a Google Cloud Project](#step-1-create-a-google-cloud-project)
  - [Step 2: Set Up OAuth Consent Screen](#step-2-set-up-oauth-consent-screen)
  - [Step 3: Create OAuth Client ID](#step-3-create-oauth-client-id)
  - [Step 4: Enable Google Sheets API](#step-4-enable-google-sheets-api)
- [Capabilities of the Google Sheets API](#capabilities-of-the-google-sheets-api)
- [Python Libraries for Google Sheets](#python-libraries-for-google-sheets)
- [Running the Program](#running-the-program)
- [Conclusion](#conclusion)

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

## Capabilities of the Google Sheets API
Here's a list of impressive capabilities that the Google Sheets API offers:

- **Read and Write Data**: Access and modify spreadsheet data programmatically.
- **Batch Updates**: Perform multiple updates to a spreadsheet in one request to optimize performance.
- **Formatting**: Apply text, cell, and number formatting to make your sheets visually appealing.
- **Conditional Formatting**: Set up rules to highlight cells automatically based on their values.
- **Data Validation**: Implement rules to restrict data entry to specific formats or values.
- **Pivot Tables**: Create and manage pivot tables to summarize data dynamically.
- **Charts and Graphs**: Generate charts from data to visualize trends and comparisons.
- **Filters and Sorting**: Apply filters and sort data programmatically.
- **Cell Merging**: Merge and unmerge cells for custom layouts.
- **Named Ranges**: Create named ranges for easier data management and referencing.
- **Protected Sheets and Ranges**: Set permissions to protect certain parts of the sheet from editing.
- **Add Sheets and Tabs**: Create and delete individual sheets within a spreadsheet.
- **Comments and Notes**: Add or modify comments to provide context for specific cells.
- **Custom Formulas**: Insert and evaluate custom formulas as needed.
- **Real-time Collaboration**: Integrate with other apps to support simultaneous edits and updates.

These features make the Google Sheets API a powerful tool for automating workflows, managing data efficiently, and enhancing collaboration.

## Python Libraries for Google Sheets
The main Python library used to work with Google Sheets is:

### `google-api-python-client`

**Features**:
- Provides comprehensive functionality for interacting with Google services, including Sheets.
- Supports reading and writing data, formatting, batch updates, and more.
- Requires OAuth 2.0 authentication for secure data access.

### Other Supporting Libraries:
- **`google-auth`**: Manages authentication.
- **`google-auth-oauthlib`**: Handles OAuth 2.0 authorization flow.
- **`google-auth-httplib2`**: Integrates authentication with HTTP for API requests.

These libraries, combined, allow you to create Python applications that can seamlessly interact with Google Sheets for various automation tasks.

## Running the Program
- Run the script:
  ```bash
  python app.py
  ```
- Enter the data as prompted to test the AI agent's ability to populate the Google Sheet.
- Type `exit` to stop the program.

## Conclusion
This project demonstrates how to integrate Python, Ollama, and the Google Sheets API to build an AI-powered data entry tool. With the outlined capabilities and detailed setup, it can be adapted for various use cases such as managing contact lists and tracking job applications.

