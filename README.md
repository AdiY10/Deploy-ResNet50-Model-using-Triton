# Deploy ResNet50 Model using Triton

This guide provides step-by-step instructions for establishing an inference infrastructure to deploy deep learning pipelines utilizing the Triton server. The purpose is to deploy a ResNet50 model and leverage the Triton server for efficient inference.

## Prerequisites
1. Machine with an NVIDIA GPU (I used Nvidia Geforce MX150).
2. CUDA Toolkit installed.
3. Docker installed.
4. Internet access.

## Steps to Deploy ResNet50 Model using Triton
1. Download Triton Client and Server Containers
2. Download ResNet50 Model Weights
3. Configure and Run Triton Server

### Step 1: Download Triton Client and Server Containers
- Go to the [NGC registry]((https://catalog.ngc.nvidia.com/orgs/nvidia/containers/tritonserver)) and download the Triton client and server containers compatible with your GPU.
- Follow the documentation provided by Triton to install and configure the containers.

### Step 2: Download ResNet50 Model Weights
- Download the [ResNet50 model weights](https://github.com/onnx/models/tree/main/vision/classification/resnet) in the ONNX format from.

### Step 3: Configure and Run Triton Server
- To use Triton, you will need to build a model repository that follows a specific structure. Here's an example structure of a Triton model repository:
```
model_repository
|
+-- resnet
    |
    +-- config.pbtxt
    +-- 1
        |
        +-- model.onnx
```
- launch a Docker container with the Triton server, making the model repository accessible to it. (change <xx.yy> to the version you need)
```
docker run --gpus all --rm -p 8000:8000 -p 8001:8001 -p 8002:8002 -v ${PWD}/model_repository:/models nvcr.io/nvidia/tritonserver:<xx.yy>-py3 tritonserver --model-repository=/models
```
- launch an interactive shell within a Docker container based on the Triton server (allows you to access and work within the Triton server environment)
```
docker run -it --rm --net=host -v ${PWD}:/workspace/ nvcr.io/nvidia/tritonserver:<yy.mm>-py3-sdk bash
```

### Step 4: Configure a Triton Client to Query the Server
- Once the Triton server is running, use a Triton client compatible with your chosen backend framework (ONNX in this case) to send classification requests.
- To view an example client notebook, refer to the [rn50_client.ipynb](rn50_client.ipynb) file.

## Conclusion
By following these steps, you should be able to successfully deploy the ResNet50 model using the Triton server. 

For more information and advanced configurations, refer to the Triton documentation and resources available on the NVIDIA Developer website.

Please note that this README provides a basic overview of the deployment process. You may need to adapt the steps based on your specific environment and requirements.
