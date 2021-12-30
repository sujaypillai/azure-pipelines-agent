# Introduction
This project holds 2 dockerfiles to generate custom Azure Pipelines Agent docker images

# Getting Started
To run a Azure Pipelines agent on Ubuntu 20.04 for a specific account with a custom agent name, pool and a volume mapped agent work folder:

```
AZP_URL=https://dev.azure.com/sujayopillai0096
AZP_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
AZP_AGENT_NAME=DockerAgentLocal

docker run -e AZP_URL=$AZP_URL \
           -e AZP_TOKEN=$AZP_TOKEN \
           -e AZP_AGENT_NAME=$AZP_AGENT_NAME \
           -v /var/run/docker.sock:/var/run/docker.sock \
           -v /var/vsts:/var/vsts \
           sujaypillai/vstsagent
```

### `docker` images
The derived images from `Dockerfile` & `Dockerfile.19.03` include a version of the Docker CLI and a compatible version of the Docker Compose CLI. This image cannot run most of the built-in VSTS build or release tasks but it can run tasks that invoke arbitrary Docker workloads.

These images do not run "Docker in Docker", but rather re-use the host instance of Docker. To ensure this works correctly, volume map the host's Docker socket into the container as shown above.


# Links
Below are the some important links to refer:
- [Azure Pipelines Agent Releases](https://github.com/Microsoft/azure-pipelines-agent/releases)
- [Run Azure Pipelines in Linux Container](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#linux)
- [Docker Hub image](https://hub.docker.com/repository/docker/sujaypillai/vstsagent)
