# HSN Code Validation Agent Using ADK Framework
 
# Agent Design & ADK Components

Overall Architecture
The HSN Code Validation Agent is built using the ADK framework to serve as an intelligent validator for HSN and SAC codes. The agent allows users to input codes and receive structured validation results in real-time.

# ADK Components
Component	Description
* Intents	Validate HSNCode, ValidateSACCode, HelpIntent
* Entities	HSNCode (2–8 digit), SACCode (2–6 digit)
* Fulfillment	Webhook connected to a Python backend that performs code validation
* Data Store	External Excel file (two sheets) parsed and loaded using Pandas
* Responses	Natural language responses with validation result, description, and reason


# Data Handling Strategy & Validation Logic
# Data Handling Strategy
* Data Source: HSN_SAC.xlsx with two sheets:
* Sheet 1: HSN codes (HSNCode, Description)
* Sheet 2: SAC codes (SACCode, SAC_Description)
  * Access Method: pandas.read_excel() to load both sheets into memory as DataFrames.
# Strategy:
* Data is pre-processed once on agent initialization to ensure fast runtime queries.
* Strip leading/trailing whitespace.
* Convert code columns to string to preserve formatting (e.g., leading zeros).
# Validation Logic
* Format Validation
* HSN codes:
* Must be numeric.
* Length must be 2, 4, 6, or 8 digits.
* SAC codes:
* Must be numeric.
* Length between 2 to 6 digits.
* Existence Validation
•	The input code is matched exactly against the respective column (HSNCode or SACCode) using a vectorized Pandas lookup.

# Steps to Build the Agent Using ADK

# Step 1: Define Agent and Intent Schema
* Create the agent using ADK with intents like ValidateHSNCode and ValidateSACCode.
* Configure entities to capture the user input (HSN/SAC codes).
# Step 2: Setup Fulfillment (Backend)
* Build a Python Flask or FastAPI server.
* Connect the /validate endpoint to handle input JSON and return code validation results.
# Step 3: Integrate Dataset
* Use pandas to load the Excel file.
* Maintain the dataset in memory for fast lookup.
# Step 4: Implement Validation Logic
* Apply format and existence checks.
* Return a structured JSON response with valid, description, or reason.
# Step 5: Connect Fulfillment to ADK
* Link the webhook to the intent fulfillment in the ADK agent configuration.
# Step 6: Test and Deploy
* Validate handling of edge cases like:
* Malformed input
* Codes with missing descriptions
* Codes that match partially
