# Deploy ResNet50 Model using Triton

This guide provides step-by-step instructions for establishing an inference infrastructure to deploy deep learning pipelines utilizing the Triton server. The purpose is to deploy a ResNet50 model and leverage the Triton server for efficient inference.

## Prerequisites
1. Machine with an NVIDIA GPU (I used Nvidia Geforce MX150).
2. CUDA Toolkit installed.
3. Docker installed.
4. Internet access.

## Steps to Deploy ResNet50 Model using Triton

### Step 1: Download Triton Client and Server Containers
- Go to the [NGC registry]([link](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/tritonserver)) and download the Triton client and server containers compatible with your GPU.
- Follow the documentation provided by Triton to install and configure the containers.

### Step 2: Download ResNet50 Model Weights
- Download the [ResNet50 model weights]([link]https://github.com/onnx/models/tree/main/vision/classification/resnet) in the ONNX format from.

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

- Open a terminal and navigate to the directory where you installed the Triton server containers.
- Start the Triton server with the appropriate command, specifying the model repository and other necessary configurations.
- Refer to the Triton documentation for detailed instructions on server configuration.

### Step 4: Use the ONNX Backend for Classification Requests
- Once the Triton server is running, you can use the ONNX backend to send classification requests.
- Write a script or use an API client to interact with the Triton server and send classification requests using the ResNet50 model.
- Ensure that the input data is properly preprocessed and formatted according to the model's requirements.
- Parse and analyze the output predictions received from the Triton server.

## Conclusion
By following these steps, you should be able to successfully deploy the ResNet50 model using the Triton server. Feel free to explore further functionalities and optimizations provided by Triton to enhance your deep learning inference pipeline.

For more information and advanced configurations, refer to the Triton documentation and resources available on the NVIDIA Developer website.

Please note that this README provides a basic overview of the deployment process. You may need to adapt the steps based on your specific environment and requirements.
