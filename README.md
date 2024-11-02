# Specialized-.NET-Razor-Web-Project-GTPs
A GitHub-integrated bot that assists with repository navigation, file retrieval, and content analysis for streamlined project development.

---

## Overview

This bot, built on OpenAI’s GPT capabilities, is designed to facilitate and enhance project development by providing seamless access to a GitHub repository's content. It enables users to list files, retrieve specific documents, and perform content analysis directly from the repository. 

Ideal for projects that leverage .NET, Razor, and Blazor, the bot integrates with GitHub to retrieve up-to-date information on the repository structure, simplifying navigation and management of project files.

---

## Key Features

- **Repository Navigation**: Easily list all files and directories in the repository.
- **File Retrieval**: Retrieve and display specific files from the repository upon request.
- **Cache and State Management**: Maintains a local cache of the repository structure for efficient access, reducing unnecessary API calls.
- **Session State Preservation**: Tracks repository updates and reloads the session context at the start of each new session.
- **Content Analysis**: Allows content inspection and analysis based on user requests, supporting detailed project exploration.

---

## How to Set Up the Bot and GitHub Action

Follow these steps to configure the bot and set up the necessary GitHub Action for integration.

### Step 1: Create the GitHub Action

1. **Add Workflow Directory**: In your GitHub repository, create a folder structure `.github/workflows/`.
2. **Create the Workflow File**: Inside `.github/workflows/`, create a file named `list-repo-content.yml`.
3. **Define the Workflow**: Configure this file to set up a GitHub Action that lists all files in the repository. This action should:
   - Run automatically on `push` to the `main` branch.
   - Be executable manually via a "workflow_dispatch" trigger.
   - Use GitHub’s `GITHUB_TOKEN` to access the repository.

> **Note**: The GitHub Action will interact with the repository to retrieve file structures recursively. Ensure that your action includes a step to access the repository tree via GitHub’s API, handling authentication with the `GITHUB_TOKEN` secret.

### Step 2: Set Up GitHub Personal Access Token (PAT)

1. **Create a PAT** in GitHub with the following permissions:
   - **repo**: Full control of private repositories.
   - **workflow**: To trigger and manage GitHub Actions workflows.
2. **Add the PAT to Repository Secrets**:
   - Go to **Settings** > **Secrets** > **Actions** in your repository.
   - Create a new secret named `GITHUB_TOKEN` and paste the PAT value here.
   
   > **Important**: The `GITHUB_TOKEN` will be used by the bot to authenticate GitHub API requests. Ensure the token permissions are set to avoid access issues.

---

### Step 3: Configure the Bot in OpenAI

1. **Create a new Custom GPT** in the OpenAI platform and go to the action configuration section.
2. **Add OpenAPI Schema**: Use the following structure to define the API schema that the bot will use to interact with GitHub:

   - **Authorization**: Configure `bearerAuth` with `JWT` as the format to match GitHub's security requirements.
   - **Endpoints**:
     - Trigger the workflow dispatch for repository listing.
     - Retrieve workflow runs and logs (optional, based on use case).

3. **Commands**:
   - `/read repo`: Lists all files and folders in the repository.
   - `/read <file name>`: Retrieves and displays a specific file's contents.

---

### Step 4: Usage Instructions

- **To List All Repository Contents**: Enter `/read repo` in the bot’s chat. The bot will trigger the GitHub Action and return a structured list of all files and directories.
- **To Retrieve a Specific File**: Enter `/read <file name>`. The bot will locate the specified file, confirm with you, and display the content upon approval.

---

### Troubleshooting

- **Permissions Error**: If you encounter issues with the bot accessing the repository, ensure that the PAT has the correct permissions and is correctly saved as a GitHub secret.
- **404 Error for Workflow**: Verify that the workflow file name and path are correct in `.github/workflows/`.
- **Large Response Handling**: For repositories with large numbers of files, consider modifying the action to limit or paginate results.

---

This setup creates a streamlined GitHub-integrated bot that supports efficient project navigation and content retrieval, enhancing collaboration within the GitHub ecosystem.
