In order to use the Image and Chat Completion features in Markdown Monster you have to configure the required OpenAI providers for image generation and one for chat completions. You can create multiple providers for each and switch between providers which can be useful to switch between local and online models.

In order to do this you'll need one of the following:

* OpenAI Account (ApiKey, ModelId)
* Azure OpenAI Deployment (ApiKey, Deployment name and Site Url)
* Ollama with local models (ModelId)
* Generic OpenAI API

> Dall-E Image generation only works with the OpenAI and Azure OpenAi online models, while Chat Completions can use local models. For local Chat Completion we recommend using [Ollama](https://ollama.com/) to expose a local OpenAI interface.

## The OpenAI Provider Configuration Form
The configuration lets you configure connections to both the Image and Chat Completion providers. Both use the same interface and depending on which provider you choose to add, different options are required for each provider *(see provider specific configuration below)*.

![](/images/OpenAiConfigurationNew.png)

You can make changes to the configuration which updates settings immediately. Click Save to persist settings into the configuration file and save settings across Markdown Monster sessions.

When creating new providers you can choose from multiple provider types:

![](/images/OpenAiConfiguration-NewProvider.png)

And you can create and switch between multiple providers for both completion and images:

![](/images/OpenAiConfiguration-MultipleProviders.png)

For completions you can choose from:

* OpenAI
* Azure OpenAI
* Ollama
* Generic OpenAI Provider

For images you can choose from:

* OpenAI
* Azure OpenAI

More advanced users can also edit the AI Provider configuration as raw JSON using the **Edit Configuration** button.

### OpenAI Configuration (Image and Completions)
OpenAI uses a single configuration for both images and chat completions - you specify which is used based on the model used (ie. dall-e-3 or any of the other `gpt-` models). 

To configure you'll need to provide:

* **Api Key**
* **Chat Model Id**: gpt-4o-mini*, gpt-3.5-turbo, gpt-4 etc.
* **Image Model Id**: dall-e-3
* **Endpoint**: https://api.openai.com/v1/

> The Endpoint and model are pre-set automatically when you create a new OpenAI connection - `dall-e-3` for images, and `gpt-4o-mini` for completions. You can change to [different OpenAI models](https://platform.openai.com/docs/models) if you like.

OpenAI Links:
* [Signup](https://platform.openai.com/signup)
* [Models and Model Ids](https://platform.openai.com/docs/models)
* [Model Pricing](https://openai.com/api/pricing/)


### Azure OpenAI Provider Configuration (Image and Completion)
Azure uses a more complex configuration for running your own models, by basically requiring you to set up a dedicated AI Web site and one or more **Deployments** for each model that you want to run. This means you are responsible for setting up an Azure OpenAI resource and then adding one ore more model deployments to the resource. You can test it in the Azure AI Studio.

For Azure OpenAI you'll need to provide the following:

* **Api Key**
* **Site Endpoint Url**: `https://YourAzureSiteName.openai.azure.com/`
* **Model Id**: Use the Deployment Name - Each Model runs in its own deployment
* **API Version**: In Azure AI Studio you can find the Preview version in the JSON test URL    
*we provide a default api version, but to get the latest updates you might want to change that to the current version*
* **EndPoint Template**: `{0}/openai/deployments/{2}/{1}?api-version={3}` 
    <small>  
    * **{0}** - Site Endpoint Url
    * **{1}** - Operation Endpoint (ie. `/images/generation/` or `/chat/completions/`)
    * **{2}** - Deployment
    * **{3}** - API revision
    </small>

> Note the Site Endpoint Url **is not the full URL** that is shown in Azure OpenAI Studio, but the **Site Base Url** for the Azure OpenAI Web site. It'll typically be `https://resourcesetname.openai.azure.com`.

### Ollama Local Model Configuration
You can also run local models using the [Ollama](https://ollama.com/) AI engine. Ollama can run models locally and exposes a local optional OpenAI service. 

You essentially **pull** down a model, and then run Ollama with a specific model by using `ollama serve` or `ollama run phi3`. Popular local models are **llama3**, **phi3**, **mistral**, **mistral-nemo** but you can find [many more models](https://ollama.com/library) to play with from Hugging Face and other AI repositories.

To run with Ollama

* **Pull a model:** with `ollama pull llama3`
* **Select a Model** with `ollama run llama3` 
* **Start Ollama with current model:** with `ollama serve` to run the OpenAI server with active model

The Ollama server `model` parameter corresponds to the name of any of the installed and previously pulled local models.

For Ollama configuration you:

* **Start Ollama:** `ollama serve`
* **Endpoint:** http://127.0.0.1:11434/v1/
* **Model Id:** Name of any locally installed model (llama3, phi3 etc.)   
*Use `ollama list` to see installed models*

> The Endpoint is set automatically when you choose Ollama for a new Completion provider and local models don't require an API key.

You can also use Ollama interactively using [OpenWebUi](https://openwebui.com/) which is a Docker based local Chat UI that lets you run Ollama models using a common Web based chat interface. It also lets you select from available models, and lets you fine tune and save models interactively.

* [Ollama Download](https://ollama.com/)
* [Open WebUI](https://github.com/open-webui/open-webui)
* [Ollama curated Models](https://ollama.com/library)
* [More models at Hugging Face Models](https://huggingface.co/models)