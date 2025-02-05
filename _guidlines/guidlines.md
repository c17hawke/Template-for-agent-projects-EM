# Agent Project Submission Requirements

Kindly adhere to the following guidelines before submitting the Agent based projects. 

## Required Documentation

Your project must include comprehensive documentation in the `README.md` file with the following sections:

### 1. Project Overview

- Clear problem statement describing the challenges the agent addresses
- Detailed explanation of the solution approach

### 2. Technical Architecture

- Block diagram illustrating the project workflow (created using `drawio` or `ExcaliDraw`)
- Step-by-step explanation of each component in the workflow diagram
- Information about the:
    - Large Language Model (LLM) used in development
    - Agent framework implementation details

### 3. Setup and Installation

- Required Python version
- Step-by-step setup instructions
- Environment variables configuration guide

## Technical Requirements

### 1. Configuration Files

- `.env.template` file listing all required environment variables
- `requirements.txt` file with pinned dependency versions

### 2. Prompt Management

All prompts must be externalized from the code and stored in a YAML file:

- Create a separate `prompts.yaml` file in the project
- Structure prompts by their use case or function
- Include clear descriptions for each prompt (Optional)
- No hardcoded prompts in the Python code

Example `prompts.yaml` structure for reference only:

```yaml
task_analysis:
  description: "Prompt for analyzing user tasks"
  content: |
    Analyze the following task and break it down into steps:
    {task_description}

agent_response:
  description: "Template for agent's responses to user queries"
  content: |
    Given the context: {context}
    Respond to: {user_query}

```

### 3. Logging Implementation

The project must implement comprehensive logging with the following levels:

- INFO: General operational information
- DEBUG: Detailed debugging information
- WARNING: Warning messages for potential issues
- ERROR: Error messages for serious problems
- EXCEPTION: Full exception traces for critical failures

All logs should be properly configured to capture runtime events and assist in monitoring and troubleshooting.

### 4. Exception Handling

The project must include basic error handling to manage problems that might occur during execution:

1. Use try-except blocks to handle common errors:

```python
try:
    # Your code here
    response = openai.ChatCompletion.create(...)
except openai.error.APIError as e:
    # Log the error
    logger.error(f"OpenAI API error occurred: {str(e)}")
    # Provide a user-friendly message
    print("Sorry, there was a problem connecting to the AI service")

```

1. Create simple custom errors for your project:

```python
class AgentError(Exception):
    """Base error for agent-related issues"""
    pass

class ConfigError(AgentError):
    """Error when configuration is missing or invalid"""
    pass

```

1. Basic error handling guidelines:
- Always include error messages that explain what went wrong
- Log errors so you can debug them later
- Handle at least these common scenarios:
    - API connection errors
    - Missing configuration or environment variables
    - File not found errors
    - Invalid input data
- Clean up resources (close files, connections) using try-finally when needed