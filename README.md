# WSO2 API Manager deployment with API Manager Analytics

## Prerequisites

 * Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), [Docker](https://www.docker.com/get-docker) and [Docker Compose](https://docs.docker.com/compose/install/#install-compose)
   in order to run the steps provided in following Quick start guide. <br><br>
 * In order to use Docker images with WSO2 updates, you need an active WSO2 subscription.
   Otherwise, you can proceed with Docker images available at [DockerHub](https://hub.docker.com/u/wso2/), which are created using GA releases.<br><br>
 * If you wish to run the Docker Compose setup using Docker images built locally, build Docker images using Docker resources
   available from [here](../../dockerfiles/) and remove the `docker.wso2.com/` prefix from the base image (i.e. `FROM` instruction) in the [Dockerfiles](dockerfiles). <br><br>
* If you don't have a valid WSO2 Subscription, you can replace the images in [dockerfiles](../apim-with-analytics/dockerfiles/) with the [public image](https://hub.docker.com/repository/docker/wso2/wso2am) (`wso2/wso2am:4.1.0`). <br><br>
* If you are trying this out on Apple Silicon (with M1), use the public image that supports arm64 architecture (`wso2/wso2am:4.1.0-multiarch`). <br><br>

## Quick Start Guide

1. Login to WSO2's Private Docker Registry via Docker client. When prompted, enter the username and password of your WSO2 Subscription.

   ```
   docker login docker.wso2.com
   ```

2. Clone WSO2 API Management Docker and Docker Compose resource Git repository.

   ```
   git clone https://github.com/wso2/docker-apim
   ```
   
   > If you are to try out an already released zip of this repo, please ignore this 2nd step. 

3. Switch to `docker-compose/apim-with-analytics` folder.

   ```
   cd docker-apim/docker-compose/apim-with-analytics
   ```
   > If you intend to try out an already released zip of this repository, extract the zip file and directly browse to
   `docker-apim-<released-version-here>/docker-compose/apim-with-analytics` folder. 
     
   > If you intend to try out an already released tag, after executing 2nd step, checkout the relevant tag, 
    i.e. for example: `git checkout tags/v4.1.0.1`, switch to `docker-compose/apim-with-analytics` folder and continue with below steps.

4. WSO2 no longer provides an on-premise Analytics solution. In order to connect WSO2 API Manager to [Choreo Analytics](https://analytics.choreo.dev/), obtain an `on-prem-key` by following the steps in the [documentation](https://apim.docs.wso2.com/en/4.1.0/observe/api-manager-analytics/configure-analytics/register-for-analytics/).

5. Update the analytics configurations in [deployment.toml](./conf/apim/repository/conf/deployment.toml) with the `on-prem key` obtained.

    ```toml
    [apim.analytics]
    enable = true
    config_endpoint = "https://analytics-event-auth.choreo.dev/auth/v1"
    auth_token = "<on-prem-key>"
    ```

6. Execute following Docker Compose command to start the deployment.

   ```
   docker-compose up --build
   ```

7. Access the WSO2 API Manager web UIs using the below URLs via a web browser.

   ```
   https://localhost:9443/publisher
   https://localhost:9443/devportal
   https://localhost:9443/admin
   https://localhost:9443/carbon
   ```
   Login to the web UIs using following credentials.
   
   * Username: admin <br>
   * Password: admin

   Please note that API Gateway will be available on following ports.
   ```
   https://localhost:8243
   https://localhost:8280
   ```
