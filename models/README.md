This folder is where your models will be saved.

Models can now be downloaded for you by LocalAI using two methods.

## Method 1: Using the Model Gallery

Step one is to register the galleries you want to use in the GALLERIES environment variable. See [`.env`](../sample.env) or [`docker-compose.yaml`](../docker-compose.yaml) files for this property. 

```bash
# Add the official sample model gallery:
GALLERIES=[{"name":"model-gallery", "url":"github:go-skynet/model-gallery/index.yaml"}, {"name":"huggingface", "url": "github:go-skynet/model-gallery/huggingface.yaml"}]
```

Here two galleries are referenced. Th official gallery from LocalAI containing free models and the unofficial list of compatible HuggingFace models. Each has a corresponding YAML file that lists all the models known to that gallery.

The download of a model is then triggerd by making a POST request to the `/models/apply` endpoint asking for the model by it's model ID. See [`setup-models.http`](../setup-models.http).

```
###
# Download the VMware LLAMA model (GGML version).
POST http://localhost:8080/models/apply HTTP/1.1
content-type: application/json

{         
     "id": "huggingface@thebloke__open-llama-7b-open-instruct-ggml__open-llama-7b-open-instruct.ggmlv3.q8_0.bin",
     "name": "gpt-3.5-turbo"
}
```

In the above example, the VMware Open Instruct model in GGML format would be downloaded from The Bloke's repository. This download method also creates a prompt template and allows for the model to be renamed to `gpt-3.5-turbo` help ChatBot-UI. 


> Note: Only a few models are listed in the official gallery [index.yaml](https://github.com/go-skynet/model-gallery/blob/main/index.yaml). The huggingface gallery [huggingface.yaml]((https://github.com/go-skynet/model-gallery/blob/main/huggingface.yaml) has more but it's not a complete list and the licence situation is less clear.

## Method 2: Using the Preload Model feature

The preload models feature can grab the binary file for a model based on a spec file you provide. To activate this feature you set the `PRELOAD_MODELS` environment variable in `.env` or in `docker-compose.yaml` to the location of a spec file like this:

```bash
# Add the Code Llama Instruct 7B model
'PRELOAD_MODELS=[{"url": "github:go-skynet/model-gallery/codellama-7b-instruct.yaml", "name": "gpt-3.5-turbo"}]
```

In this example, the Code Llama Instruct model with 7b parameters will be downloaded based on the spec in the [`codellama-7b-instruct.yaml`](https://github.com/go-skynet/model-gallery/blob/main/codellama-7b-instruct.yaml) file in the model-gallery repository. The necessary prompts will also be setup based on the details in the spec.

# HuggingFace Gallery Models To Try:

"huggingface@thebloke__open-llama-7b-open-instruct-ggml__open-llama-7b-open-instruct.ggmlv3.q8_0.bin"

