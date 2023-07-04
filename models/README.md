This folder is where your models will be saved.

Models can now be downloaded for you by LocalAI using the "Model Galleries" feature in v1.20. Models can come from the official model gallery, or from HuggingFace. The galleries are setup using an environment variable. See `.env` or `docker-compose.yaml`. 

They download is triggerd by making a REST POST request to the `/models/apply` endpoint. See `setup-models.http`.

Models to try:

"huggingface@thebloke__open-llama-7b-open-instruct-ggml__open-llama-7b-open-instruct.ggmlv3.q8_0.bin"

Downloaded "open-llama-7B-open-instruct.ggmlv3.q8_0.bin" and rename it to "open-llama-7B-open-instruct". Set this as the default model for ChatBotUI in the `docker-compose.yaml`.

