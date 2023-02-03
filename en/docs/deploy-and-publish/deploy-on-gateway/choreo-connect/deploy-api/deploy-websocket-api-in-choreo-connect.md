# Deploying a WebSocket API in Choreo Connect

You can deploy a WebSocket type API in Choreo Connect using [Choreo Connect with WSO2 API Manager as a Control Plane](#choreo-connect-with-wso2-api-manager-as-a-control-plane).

## Choreo Connect with WSO2 API Manager as a Control Plane

Follow the instructions below to use Choreo Connect with WSO2 API Manager as the Control Plane to deploy a WebSocket type Streaming API via the Publisher Portal in WSO2 API Manager:

!!! info
    **Before you begin**

    This guide assumes that you already have a Choreo Connect 1.0.0 instance that is up and running. If not, checkout the [Quick Start Guide]({{base_path}}/deploy-and-publish/deploy-on-gateway/choreo-connect/getting-started/quick-start-guide-docker-with-apim/) on how to install and run Choreo Connect. To learn more about Choreo Connect, have a look at the [Overview of Choreo Connect]({{base_path}}/deploy-and-publish/deploy-on-gateway/choreo-connect/getting-started/choreo-connect-overview).


!!! note
    **Limitations compared to WSO2 API Manager 4.0.0**

    WSO2 API Manager allows users to provide multiple topics per Websocket API. In contrast, Choreo Connect 1.0.0 does not support topics currently. The inbound request URL follows the structure `<choreo-connect-gateway-url>/<API-Context>/<Version>`. And internally, the request will be forwarded to the API's endpoint URL with no topic appended to the end of the URL.


### Step 1 - Create a WebSocket API in API Manager

 For instructions on how to create a WebSocket API, see [Create a WebSocket API]({{base_path}}/design/create-api/create-streaming-api/create-a-websocket-streaming-api/).

### Step 2 - Deploy the API in the Choreo Connect environment

For more information on deploying the API in Choreo Connect, see [Deploy API]({{base_path}}/deploy-and-publish/deploy-on-gateway/deploy-api/deploy-an-api/).

### Step 3 - Generate an Access Token to invoke the API

By default, the WebSocket API is protected by an OAuth2 token.

For more information on generating a JWT Access token, see [Get a Test Key to Invoke an API]({{base_path}}/consume/invoke-apis/invoke-apis-using-tools/invoke-an-api-using-the-integrated-api-console/#get-a-test-key-to-invoke-an-api).

### Step 4 - Invoke the API using a WebSocket client

The WebSocket API exposed via Choreo Connect can be invoked by using a WebSocket client.
The JWT token should be set as the Authorization header in the initial WebSocket handshake request.

!!!note
    The same ports 9095 (HTTPS) and 9090 (HTTP) are used for WebSocket APIs.

Invoke the WebSocket API by carrying out [Step 4]({{base_path}}/tutorials/streaming-api/create-and-publish-websocket-api/#step-4-invoke-the-websocket-api) in the Create and Publish a WebSocket API tutorial.
