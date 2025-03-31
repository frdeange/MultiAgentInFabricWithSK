# Multi-Agent System in Microsoft Fabric with Semantic Kernel

## Overview

This project demonstrates how to orchestrate multiple specialized AI agents inside a Microsoft Fabric notebook using the Semantic Kernel framework and Azure AI Agent Service. The system implements a decomposition and recomposition approach with:

1. A **Router Agent** that analyzes user queries and delegates to specialized agents
2. Multiple **Domain Expert Agents** that handle specific query aspects
3. A **Synthesis Agent** that combines responses into a cohesive answer

## Architecture

The system follows this workflow:
1. User submits a query to the Router Agent
2. Router determines which specialist agents should handle different parts of the query
3. Each specialist agent processes its assigned sub-query independently
4. All responses are collected and sent to the Synthesis Agent
5. The Synthesis Agent combines the information into a unified response

## Components

- **Router Agent**: Routes user queries to appropriate domain expert agents
- **Synthesis Agent**: Combines responses from multiple agents
- **Domain Expert Agents**:
  - **CustomerInfoAgent**: Handles customer data queries using Fabric AI Skill
  - **MarketingAgent**: Generates creative marketing content
  - **LoyaltyProgramsAgent**: Provides information about Power Platform licensing via Azure AI Search
  - **ChitChatAgent**: Handles general conversational queries

## Prerequisites

### 1. Azure AI Foundry Resource

You need to create an Azure AI Foundry resource to deploy and manage your agents:

1. Go to the [Azure Portal](https://portal.azure.com)
2. Create a new "Azure AI Foundry" resource in your subscription
3. Select an appropriate region and pricing tier
4. Once deployed, navigate to the resource and create a new project
5. Note the project connection string for configuration in your notebook
6. Ensure you have the necessary quota for the models you plan to use (e.g., GPT-4o)

For detailed instructions, refer to the [Azure AI Foundry documentation](https://learn.microsoft.com/en-us/azure/ai-studio/what-is-ai-studio).

### 2. Azure Tenant Application Registration

You need to create an application registration in your Azure tenant:

1. Go to [Azure Portal](https://portal.azure.com) > "Azure Active Directory" > "App Registrations"
2. Click "New registration"
3. Provide a name for your application
4. Select "Accounts in this organizational directory only" for supported account types
5. Click "Register"
6. From the overview page, note the **Application (client) ID** and **Directory (tenant) ID**
7. Under "Certificates & secrets", create a new client secret and note the **Value**
8. Assign appropriate permissions to access Azure AI and Microsoft Fabric resources

For detailed instructions, refer to the [official documentation](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app).

### 3. Microsoft Fabric Environment

You need access to a Microsoft Fabric environment:

1. Ensure you have a Fabric F64 capacity or higher
2. Create a new workspace with Data Science persona enabled
3. Set up proper permissions for all team members

### 4. Fabric AI Skill

Create an AI Skill in your Fabric environment:

1. In your Fabric workspace, create a new AI Skill
2. Configure the skill with appropriate data sources
3. Test the skill to ensure it works correctly
4. Note the AI Skill URL for programmatic access

For detailed instructions, follow the [official guide on AI Skills in Fabric](https://learn.microsoft.com/en-us/fabric/data-science/ai-skill-scenario#use-the-ai-skill-programmatically).

### 5. Azure AI Search Index

Set up an Azure AI Search Index for the LoyaltyProgramsAgent:

1. Create an Azure AI Search service
2. Create an index with Power Platform licensing information
3. Connect your Fabric environment to the search service
4. Note the index name for configuration

## Installation

### Create a Notebook in Fabric

1. In your Fabric workspace, create a new notebook
2. Clone this repository or copy the code from `MultiAgentFabricDemo.ipynb`
3. Update the environment variables in the first cell with your configuration values:
   - `ENTRAID_TENANT_ID`: Your Azure tenant ID
   - `ENTRAID_CLIENT_ID`: Your application client ID
   - `ENTRAID_SECRET`: Your application client secret
   - `AZUREAI_PROJECT_CONNECTION`: Your AI Foundry project connection string
   - `AZURE_AI_MODEL_NAME`: The model to use (e.g., "gpt-4o")
   - `FABRIC_AI_SKILL_URL`: Your Fabric AI Skill URL
   - `AZURE_AIASEARCH_INDEX_NAME`: Your Azure AI Search index name

### Install Required Libraries

Run the installation cell to install dependencies:
```python
%pip install semantic-kernel azure-ai-projects azure-identity
```

## Usage

1. Run all notebook cells sequentially
2. The system will create and configure all required agents
3. Customize the `user_message` variable to test different queries
4. The notebook will display:
   - The routing agent's decision
   - Individual responses from domain experts
   - The final synthesized response
5. Remember to run the cleanup cell at the end to delete created agents

## Example Query

```python
user_message = "Could you give a me a list of 5 customers? And give me details about power platform licensing."
```

## Important Notes

- Ensure your Azure application has the necessary permissions to access Azure AI services
- The Fabric environment must have internet connectivity to reach Azure services
- The AI Skill must be properly configured to access customer data
- Large language models like GPT-4o may incur usage costs
- For production use, implement proper error handling and monitoring

## Troubleshooting

- If agents fail to create, check your Azure credentials and permissions
- If the AI Skill returns no data, verify its configuration and accessibility
- If the AI Search tool fails, ensure your index is properly configured
- Check Fabric logs for any errors in the notebook execution
- If you receive quota errors, verify your Azure AI Foundry subscription limits

## Project Structure

- **MultiAgentFabricDemo.ipynb**: Main implementation notebook
- **README.md**: Project documentation