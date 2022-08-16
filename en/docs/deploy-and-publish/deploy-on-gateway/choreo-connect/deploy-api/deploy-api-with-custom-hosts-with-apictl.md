# Exposing APIs With Custom Hostnames in Choreo Connect Using WSO2 API Controller

Follow the instructions below to deploy an API with a custom hostname in Choreo Connect using the WSO2 API Controller (apictl), which is the CLI Tool:

!!! info
    **Before you begin**

    This guide assumes that you already have a Choreo Connect instance that is up and running. If not, checkout the [Quick Start Guide]({{base_path}}/deploy-and-publish/deploy-on-gateway/choreo-connect/getting-started/deploy/cc-on-docker-with-api-controller) on how to install and run Choreo Connect. To learn more about Choreo Connect, have a look at the [Overview of Choreo Connect]({{base_path}}/deploy-and-publish/deploy-on-gateway/choreo-connect/getting-started/choreo-connect-overview).

Follow the all steps except **Deploy API** in the (Deploy an API via apictl documentation)[{{base_path}}/deploy-and-publish/deploy-on-gateway/choreo-connect/deploy-api/deploy-api-via-apictl/].

Before deploying the API project, edit the file `deployment_environments.yaml`.

```yaml
type: deployment_environments
version: v4.0.0
data:
 -
   displayOnDevportal: true
   deploymentEnvironment: Default
   deploymentVhost: us.wso2.com
```

!!! info
    When configuring multiple Choreo Connect Gateway environments, you have to configure the default VHost of the particular environment.
    
    ```toml tab="Format"
    # default vhosts mapping for standalone mode
    [[adapter.vhostMapping]]
      environment = <ENVIRONMENT_NAME>
      vhost = <DEFAULT_VHOST_OF_ENVIRONMENT>
    ```
    
    ```toml tab="Example"
    # default vhosts mapping for standalone mode
    [[adapter.vhostMapping]]
      environment = "Default"
      vhost = "localhost"
    [[adapter.vhostMapping]]
      environment = "sg-region"
      vhost = "sg.wso2.com"
    ```
    
    If the VHost is not declared in the API project, the API is deployed with the default VHost of the environment.
    For exammple, an API project with following `deployment_environments.yaml` will be deployed to the following.
    - Environment: Default - Vhost: us.wso2.com
    - Environment: sg-region - Vhost: sg.wso2.com
    - Environment: uk-region - API is not deployed to this environment becuase it is not configured in `[[adapter.vhostMapping]]`.
    
    ```yaml
    type: deployment_environments
    version: v4.0.0
    data:
     -
       displayOnDevportal: true
       deploymentEnvironment: Default
       deploymentVhost: us.wso2.com
     -
       displayOnDevportal: true
       deploymentEnvironment: sg-region
     -
       displayOnDevportal: true
       deploymentEnvironment: uk-region
    ```

Let's invoke the API.

## Invoke the API

First we need to add the host entry to `/etc/hosts` file in order to access the API Manager publisher and Developer Portal.
Add the following entry to `/etc/hosts` file

```sh
127.0.0.1   us.wso2.com
```

{! ./includes/obtain-jwt.md !}

Execute the following cURL command to Invoke the API using the JWT.

```sh
curl -X GET "https://us.wso2.com:9095/v2/pet/findByStatus?status=available" -H "accept: application/xml" -H "Authorization:Bearer $TOKEN" -k
```

!!! note
    You can also use header to specify the VHost to invoke the API.
    ```sh
    curl -X GET "https://localhost:9095/v2/pet/findByStatus?status=available" \
        -H "Host: us.wso2.com"
        -H "accept: application/xml" \
        -H "Authorization:Bearer $TOKEN" -k
    ```
