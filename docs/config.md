# Configuring Language Models

As an administrator, you can configure Sia AI to use different large language models (LLMs) as its core engine. This allows you to switch between providers like OpenAI, Google, Anthropic, or even use a self-hosted model, depending on your organization's performance, cost, and security requirements.

## Locating the Configuration File

The LLM configuration is managed in the main configuration file for the Sia AI application.

-   **File Location:** The file is named `config.yaml` and is typically located in the root directory of your Sia AI installation.

!!! warning "Backup Before Editing"
    Always create a backup of your `config.yaml` file before making any changes. An incorrect configuration can prevent the application from starting.

## Syntax for LLM Configuration

Inside `config.yaml`, you will find a section dedicated to the language model, usually under a key like `llm` or `model_provider`. You need to specify the provider and provide the necessary credentials.

### Example 1: Using OpenAI (GPT-4)

To use an OpenAI model, you need to provide the model name and your API key.

```yaml
# config.yaml

llm:
  provider: openai
  config:
    model: "gpt-4-turbo"
    api_key: "sk-YOUR_OPENAI_API_KEY" # It is highly recommended to use an environment variable instead

```

```yaml
# config.yaml


llm:
  provider: google
  config:
    model: "gemini-1.5-pro-latest"
    api_key: "YOUR_GOOGLE_AI_STUDIO_API_KEY" # Use environment variables for production

```

```yaml
# config.yaml

llm:
  provider: openai # Many local servers use an OpenAI-compatible API
  config:
    model: "llama3-70b" # The name of the model served by your local endpoint
    api_base: "http://localhost:8000/v1" # The base URL of your local LLM server
    api_key: "not-needed" # API key can often be a dummy string for local models

```
