# Deploying Choreo Connect on Kubernetes With WSO2 API Manager as a Control Plane

Let's deploy an API on Choreo Connect, which running on Kubernetes, with WSO2 API Manager as the Control Plane.

## Before you begin

1.  Install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
2.  Set up a [Kubernetes](https://Kubernetes.io/docs/setup/) cluster v1.20 or above.
      - Minimum CPU : 4vCPU
      - Minimum Memory : 3GB
3.  Deploy an ingress controller - [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/deploy/) for this sample.

{!includes/deploy/k8s-setup-note.md!}

## Objectives

1.  Create and deploy an API project.
2.  Invoke the API using a generated key.

Let's get started...

## Step 1 - Setup Choreo Connect in Kubernetes

1.  Download and extract Choreo Connect distribution .zip file

    Latest Choreo Connect distribution can be downloaded from [https://wso2.com/choreo/choreo-connect/](https://wso2.com/choreo/choreo-connect/). Extract the Choreo Connect distribution .zip file. The extracted folder will be called as `CHOREO-CONNECT_HOME` hereafter.

2.  Add the Kubernetes configurations for Choreo Connect and API Manager using the kubectl tool.

    {!includes/deploy/cc-tryout-in-arm64-k8s-note.md!}

    ```bash
    kubectl apply -f <CHOREO-CONNECT_HOME>/k8s-artifacts/choreo-connect-with-apim/apim
    ```
    
    Apply Kubernetes configurations for Choreo Connect after successfully started the API Manager instance.
    ```bash
    kubectl apply -f <CHOREO-CONNECT_HOME>/k8s-artifacts/choreo-connect-with-apim/choreo-connect
    ```
    
3.  Add the host entry to the `/etc/hosts` file. 
    
    Add the following entry to `/etc/hosts` file in order to access the Choreo Connect Router, API Manager publisher and Developer Portal.

    ```sh
    <ingress_address>    gw.wso2.com    apim.wso2.com
    ```


## Step 2 - Deploy Sample API from API Manager

 - Publisher Portal:  [https://apim.wso2.com/publisher/](https://apim.wso2.com/publisher/)
 - Developer Portal:  [https://apim.wso2.com/devportal/](https://apim.wso2.com/devportal/)


    Follow the instructions in [create and publish an API via API Manager]({{base_path}}/deploy-and-publish/deploy-on-gateway/choreo-connect/getting-started/quick-start-guide-docker-with-apim/#step-3-create-and-publish-an-api-from-api-manager).

