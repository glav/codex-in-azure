# Using codex with Azure OpenAI Models
A simple repo to show the configuration required to use codex with Azure OpenAI Models - specifically GPT-5-codex.

**Caveat: This works as at the time of writing but may change**

# Configuration
codex requires a config file located at:
```
~/.codex/config.toml
```

## Config file contents
To use with an Azure OpenAI model, you will need to do add the following config to the ```confiug.toml``` file:

```
model = "gpt-5-codex" # Change this to match your model -deployment name- (not the model name)
model_provider = "azure"
provider = "azure"

[model_providers.azure]
name = "Azure"
# Make sure you set the appropriate subdomain for this URL.
base_url = "https://{your-openai-host}.openai.azure.com/openai"
env_key = "AZURE_OPENAI_API_KEY"  # Or "OPENAI_API_KEY", whichever you use.
query_params = { api-version = "2025-04-01-preview" }
wire_api = "responses"
model_reasoning_effort = "medium"
```

**Note:** The ```base_url``` is not clearly documented when using Azure. For example, some posts suggest using something like (note the ***v1*** on the end ):
```
base_url = "https://{your-openai-host}.openai.azure.com/openai/v1"
```
I found that this did not work and would generate errors. Additionally, the above ```base_url``` is using an older OpenAI resource. These are currently being migrated to AI Foundry and so the url parameter will need to reflect what AI Foundry uses. So something like:
```
base_url = "https://{your-foundry-host}.cognitiveservices.azure.com/openai"
```
Although I have not tested this personally at this time.

### Important
Even with the configuration above, you will need to ensure the environment variable that is specified by ```env_key = "AZURE_OPENAI_API_KEY"```  is set so you need to do:
```export AZURE_OPENAI_API_KEY={your-api-key-from-foundry-for-deployment}```

