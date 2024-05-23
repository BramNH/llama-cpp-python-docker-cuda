# llama-cpp-python Server with Functionary LLM
This repository contains the necessary files to build your own Docker image for running llama-cpp-python server (OpenAI API) in combination with the [MeetKai/functionary](https://github.com/MeetKai/functionary) LLM in a CUDA environment.

## Build image
* Clone this repository and navigate into the root folder.
```
git clone https://github.com/BramNH/llama-cpp-python-docker-cuda \
cd llama-cpp-python-docker-cuda
```
* Edit line 1 of `Dockerfile` to match your [CUDA version / Linux distribution](https://hub.docker.com/r/nvidia/cuda/tags). It must be the `devel` image.

* Build the Docker image.
```
docker build --tag llama-cpp-python .
```
* Run the container.
```
docker compose up -d
```

## Quick setup
Only do this if you meet the requirements below. Otherwise build your own image as described above.
### Prerequisites:
* You are running `Ubuntu 22.04`
* Maximum supported CUDA version 12.1 (check with command `$ nvidia-smi`).

Directly run the Docker container and load the Functionary Small v2.4 LLM from Huggingface.
```
docker run -p 8000:8000 -e USE_MLOCK=0 -e HF_MODEL_REPO_ID=meetkai/functionary-small-v2.4-GGUF -e MODEL=functionary-small-v2.4.Q4_0.gguf -e HF_PRETRAINED_MODEL_NAME_OR_PATH=meetkai/functionary-small-v2.4-GGUF -e N_GPU_LAYERS=33 -e CHAT_FORMAT=functionary-v2 -e N_CTX=4092 -e N_BATCH=192 -e N_THREADS=6 bramnh/llama-cpp-python:latest
```
