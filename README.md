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

## Technical Implementation

- Built on **Microsoft Semantic Kernel** for agent orchestration
- Uses **Azure AI Agent Service** for agent creation and management
- Integrates with **Microsoft Fabric AI Skills** for data access
- Leverages **Azure AI Search** for knowledge retrieval
- Implements asynchronous processing with proper thread management

## Requirements

- Azure subscription with access to Azure AI Services
- Microsoft Fabric workspace with AI capabilities
- Required Python packages:
  - semantic-kernel
  - azure-ai-projects
  - azure-identity
  - openai

## Getting Started

1. Set up your Azure credentials in the notebook
2. Run the notebook cells sequentially
3. The system will create and configure all required agents
4. Test with sample queries that span multiple domains

## Example Usage

```python
# Define a user query that spans multiple agent domains
user_message = "Could you give a me a list of 10 customers? And give me too details about power platform licensing."

# System will route to CustomerInfoAgent and LoyaltyProgramsAgent
# Then synthesize responses into a single coherent answer
```

## Project Structure

- **MultiAgentFabricDemo.ipynb**: Main implementation notebook
- **.env**: Configuration for Azure AI Services