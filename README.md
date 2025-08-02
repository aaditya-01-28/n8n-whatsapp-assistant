
This project is an n8n workflow designed to act as a Google Drive assistant controlled by WhatsApp messages. The goal is to allow a user to manage files and folders in their Google Drive by sending simple text commands.

The initial stages of the workflow, including receiving and parsing commands from WhatsApp, were built successfully. However, the project was ultimately blocked by an unresolvable issue with the Google Drive API connection.

## Features (Intended)

The assistant was designed to support the following commands:
* `LIST /FolderName` - List files in a specified folder.
* `DELETE /FolderName/FileName.pdf` - Delete a specified file.
* `MOVE /Source/File.pdf /Destination` - Move a file to a different folder.
* `SUMMARY /FolderName` - Provide an AI-generated summary of documents in a folder.

## Setup Instructions

1.  **Run n8n via Docker:**
    Use Docker to run your own n8n instance. You can find the necessary commands on the n8n documentation website.

2.  **Set Up Twilio Sandbox:**
    * Create a free account on Twilio.
    * Navigate to **Messaging > Try it out > Send a WhatsApp message** and connect your phone to the sandbox by sending the provided `join <your-unique-code>` message.

3.  **Set Up Google Cloud Credentials:**
    * Create a project in the Google Cloud Console.
    * Enable the **Google Drive API**.
    * Navigate to **APIs & Services > OAuth consent screen**, click **"Edit App"**, and ensure the `.../auth/drive` scope is added and your email is listed as a **Test User**.
    * Navigate to **APIs & Services > Credentials** and create an **OAuth 2.0 Client ID** for a "Web application", adding the n8n redirect URI.

4.  **Import and Configure the Workflow:**
    * Import the provided `workflow.json` file into your n8n instance.
    * Open the workflow and configure the credentials for the Twilio, Google Drive, and OpenAI nodes using the credentials you created.

## Blocker: Google Drive API Connection Issue

The workflow was built to receive WhatsApp messages and parse commands successfully. However, the connection to the Google Drive API is blocked by a persistent, unresolvable issue.

**Problem:**
The Google Drive node fails to execute write operations (like "Create Folder") silently, without providing an error message. This occurs even after a successful OAuth2 connection is established in the n8n interface.

**Troubleshooting Steps Performed:**
A series of extensive debugging steps were taken to resolve the issue, including:
* Verifying the Google Drive API was enabled in the Google Cloud Platform.
* Ensuring the OAuth Consent Screen was configured with the correct, full-access (`.../auth/drive`) scopes.
* Adding the user's email as an approved "Test User".
* Completely deleting and re-creating the OAuth 2.0 Client ID and n8n credentials from scratch to ensure a clean state.

**Conclusion:**
Despite these steps, the block persists. This suggests a deeper issue with the API permissions or the n8n cloud environment that is beyond standard configuration. This blocker prevents the implementation of the `LIST`, `DELETE`, `MOVE`, and `SUMMARY` functions.