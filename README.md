# local-ai-playground

Repo for storing my work on Local AI solutions

## UPDATE: 2023-07-12

Updated the [setup-models.http](./setup-models.http) to add the latest V2 Open LLAMA 7B V2 Open Instruct model as a model download target.

## UPDATE: 2023-07-04

Updated to the latest version of LocalAI and added the parts necessary to enable automatic download of models from HuggingFace and the Model Gallery. 

## My Notes.

This project relies heavily on Docker and Docker Compose. It's best to have at least 16GB of RAM and a Intel 11 Gen CPU (or better). No GPU is required.

The `docker-compose.yml` uses images created by:

* [LocalAI](https://github.com/go-skynet/LocalAI)
* [ChatBot UI](https://github.com/mckaywrigley/chatbot-ui)

These projects are changing rapidly. Sometimes everything works, and sometimes there are issues. For example, in v1.19 of LocalAI the Stable Diffusion image generation doesn't work (but it's fine in v1.18).

If you have issues, the [LocalAI website](https://localai.io) is a good source of information and help.

### Starting On Your Machine

To start the LocalAI/ChatBotUI application use the following command from the the root folder of this repository (the one containing this README).

```bash
docker compose up -d
```

This will pull down two docker images (one for LocalAI and one for the the ChatBot-UI). The docker containers will then start to spin up. 

This process can take a long time if you're starting the servers for the first time. LocalAI will need to download some AI models (which are quite big). Tail the logs on the LocalAI image (names `api`) to monitor progress and wait for the system to fully come up. This can take several minutes.

```bash
docker logs -f --tail 1000 local-ai-api
```

Once the system has finished initializing, you'll see the following message in the log:

```text
 ┌───────────────────────────────────────────────────┐ 
 │                   Fiber v2.47.0                   │ 
 │               http://127.0.0.1:8080               │ 
 │       (bound on host 0.0.0.0 and port 8080)       │ 
 │                                                   │ 
 │ Handlers ............ 25  Processes ........... 1 │ 
 │ Prefork ....... Disabled  PID .............. 4467 │ 
 └───────────────────────────────────────────────────┘ 
```

> The [`sample.env`](.env) file contains the ENVIRONMENT variables used by the [`docker compose`](docker-compose.yaml) command to bring up the containers. 

If you haven't done so already, you now need to download and configure a suitable large language model. See the [models README](./models/README.md) for detailed instructions.

Assuming the ChatBot-UI has also started (check with `docker ps`), you are now free to start using the application. Point your browser to [http://localhost:3001](http://localhost:3001).

You can then start using the ChatBot-UI to communicate with the model. Be patient. The model's responses can take a while depending on many factors including the model size, the CPU speed, RAM available, SSD speed etc. It can also be quite inaccurate sometimes, depending on the question, the prompt, and the context.

### Downloading Models

See [The Models README](./models/README.md) for more details.

### Using Chat

Open your bowser and navigate to [http://localhost:3001](http://localhost:3001). Here you will find [ChatBot UI](https://github.com/mckaywrigley/chatbot-ui)

### Calling The REST API Directly

The file `api-requests.http` can be used with the VS Code extension "REST Client" to send REST calls to the LocalAI backend. This is useful for working with models like Stable Diffusion where images are created rather than chats.  
