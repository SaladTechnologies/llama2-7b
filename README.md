## Benchmarking script for Salad Cloud API
This script is to benchmark the performance of the llama2-7b on Salad Portal. It makes a request to the API along with certain parameters, such as the API key, access domain name, and data. The results of the request are then saved to a file.

## How to run the script
To run the script, you will need to have Python installed. You can then save the script as a .py file and run it from the command line. For example, if you have saved the script as benchmark.py, you can run it by typing the following command into the command line:

```
python benchmark.py
```

This will run the script and save the results to a file.

## Parameters
The script requires the following parameters:

- domain_name: The domain name of the Salad Cloud API.
- api_key: The API key for the Salad Cloud API.
- data: The data to be sent to the Salad Cloud API.

## Building the Docker Image

First, [download the model](https://huggingface.co/meta-llama/Llama-2-7b/tree/main) from Huggingface. Then, run the `convert_llama_weights_to_hf.py` script to convert the model to a Huggingface format. 

```shell
python3 llama2-7b-gpu-docker/convert_llama_weights_to_hf.py \
--input_dir llama2-7b-gpu-docker/model \
--model_size tokenizer_only \
--output_dir llama2-7b-gpu-docker/model_hf
```

This will create a `model_hf` directory in the `./llama2-7b-gpu-docker` directory.

From project root:
```shell
docker build -t saladtechnologies/llama2-7b:latest -f ./llama2-7b-gpu-docker/Dockerfile ./llama2-7b-gpu-docker
```

## Running the Docker Container

```shell
docker run --gpus all -p 8888:8888 saladtechnologies/llama2-7b:latest
```