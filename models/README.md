This folder is where your models will be saved.

Models can now be downloaded for you by LocalAI using the "Model Galleries" feature in v1.20. Models can come from the official model gallery, or from HuggingFace. The galleries are setup using an environment variable. 

```bash
# Add the official sample model gallery:
GALLERIES=[{"name":"model-gallery", "url":"github:go-skynet/model-gallery/index.yaml"}]
# See the LocalAI.io website for more galleries (such as HuggingFace).
```

The download is then triggerd by making a POST request to the `/models/apply` endpoint. See [`setup-models.http`](../setup-models.http).

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

This download method also creates a prompt template and allows for the model to be renamed to help ChatBot-UI. 

See [`sample.env`](../sample.env) or [`docker-compose.yaml`](../docker-compose.yaml). 

> Note: Only a few models were listed in the official gallery [index.yaml](https://github.com/go-skynet/model-gallery/blob/main/index.yaml). Instead I used the HuggingFace unofficial gallery.

# HuggingFace Gallery Models To Try:

"huggingface@thebloke__open-llama-7b-open-instruct-ggml__open-llama-7b-open-instruct.ggmlv3.q8_0.bin"

